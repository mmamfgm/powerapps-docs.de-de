---
title: Verwenden der Hybrid-Navigation zum Rendern der Seitenhierarchie für ein Portal | MicrosoftDocs
description: Anleitungen zum Verwenden von Hybrid-Navigation zum Rendern der Seitenhierarchie für ein Portal.
author: sbmjais
manager: shujoshi
ms.service: powerapps
ms.topic: conceptual
ms.custom: ''
ms.date: 10/07/2019
ms.author: shjais
ms.reviewer: ''
ms.openlocfilehash: aace949be3cc191af5edd95c461e422b9c3217f5
ms.sourcegitcommit: 8185f87dddf05ee256491feab9873e9143535e02
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/01/2019
ms.locfileid: "2708349"
---
# <a name="render-up-to-three-levels-of-page-hierarchy-by-using-hybrid-navigation"></a>Rendern von bis zu drei Ebenen der Seitenhierarchie mithilfe der hybriden Navigation

Dieses Beispiel rendert eine hybride Navigation auf Basis der Portalsiteübersicht, die bis zu drei Ebenen der Seitenhierarchie rendert. Die Regeln für diese Komponente sind:

* Die Vorängerseiten der aktuellen Seite werden angezeigt, zurück zur Homepage (oder die maximale Tiefe wie durch den optionalen Tiefe\_Versatz-Parameter festgelegt). 
* Wenn die aktuellen Seite untergeordnete Elemente hat, werden diese untergeordneten Seiten angezeigt.
* Wenn der aktuellen Seite keine untergeordnete Elemente hat, werden die Geschwisterelemente der aktuellen Seite angezeigt.

```xml
{% assign depth_offset = depth_offset | default: 0 %}
{% assign current_page = current_page | default: page %}
{% assign current_depth = 0 %}

{% if current_page.children.size > 0 %}
  {% assign leaf_page = false %}
{% else %}
  {% assign leaf_page = true %}
{% endif %}

{% capture page_item %}
  <li class=active>
    <a href={{ current_page.url | h }} title={{ current_page.title | h }}>
      {% if leaf_page %}
        <span class=fa fa-fw aria-hidden=true></span>
      {% else %}
        <span class=fa fa-fw fa-caret-down aria-hidden=true></span>
      {% endif %}
      {{ current_page.title | h }}
    </a>
    {% unless leaf_page %}
      <ul>
        {% for child in current_page.children %}
          <li>
            <a href={{ child.url | h }} title={{ child.title | h }}>
              {% if child.children.size > 0 %}
                <span class=fa fa-fw fa-caret-right aria-hidden=true></span>
              {% else %}
                <span class=fa fa-fw aria-hidden=true></span>
              {% endif %}
              {{ child.title | h }}
              {% if child.entity.logical_name == 'adx_shortcut' %}
                &nbsp;<span class=fa fa-fw fa-external-link aria-hidden=true></span>
              {% elsif child.entity.logical_name == 'adx_webfile' %}
                &nbsp;<span class=fa fa-fw fa-file-o aria-hidden=true><span class=sr-only>(File)</span></span>
              {% endif %}
            </a>
          </li>
        {% endfor %}
      </ul>
    {% endunless %}
  </li>
{% endcapture %}

<ul class=side-nav role=navigation>
  {% assign crumb_count = 0 %}
  {% assign leaf_mode = false %}
  
  {% for crumb in current_page.breadcrumbs %}
    {% unless current_depth < depth_offset %}
      {% if forloop.last and leaf_page %}
        {% assign leaf_mode = true %}
      {% else %}
        <li>
          <a href={{ crumb.url | h }} title={{ crumb.title | h }}>
            <span class=fa fa-fw fa-caret-right aria-hidden=true></span>
            {{ crumb.title | h }}
          </a>
        </li>
      {% endif %}
      {% assign crumb_count = crumb_count | plus: 1 %}
    {% endunless %}
    {% assign current_depth = current_depth | plus: 1 %}
  {% endfor %}
  
  {% if crumb_count < 1 %}
    {{ page_item }}
  {% elsif crumb_count < 2 and leaf_mode %}
    {% for parent_sibling in current_page.parent.parent.children %}
      {% if parent_sibling.url == current_page.parent.url %}
        <li>
          <a href={{ current_page.parent.url | h }} title={{ current_page.parent.title | h }}>
            <span class=fa fa-fw fa-caret-down aria-hidden=true></span>
            {{ current_page.parent.title | h }}
          </a>
          <ul>
            {% for sibling in current_page.parent.children %}
              <li {% if sibling.url == current_page.url %}class=active{% endif %}>
                <a href={{ sibling.url | h }} title={{ sibling.title | h }}>
                  {% if sibling.children.size > 0 %}
                    <span class=fa fa-fw fa-caret-right aria-hidden=true></span>
                  {% else %}
                    <span class=fa fa-fw aria-hidden=true></span>
                  {% endif %}
                  {{ sibling.title | h }}
                  {% if sibling.entity.logical_name == 'adx_shortcut' %}
                    &nbsp;<span class=fa fa-fw fa-external-link aria-hidden=true></span>
                  {% elsif sibling.entity.logical_name == 'adx_webfile' %}
                    &nbsp;<span class=fa fa-fw fa-file-o aria-hidden=true><span class=sr-only>(File)</span></span>
                  {% endif %}
                </a>
              </li>
            {% endfor %}
          </ul>
        </li>
      {% else %}
        <li>
          <a href={{ parent_sibling.url | h }} title={{ parent_sibling.title | h }}>
            {% if parent_sibling.children.size > 0 %}
              <span class=fa fa-fw fa-caret-right aria-hidden=true></span>
            {% else %}
              <span class=fa fa-fw aria-hidden=true></span>
            {% endif %}
            {{ parent_sibling.title | h }}
            {% if parent_sibling.entity.logical_name == 'adx_shortcut' %}
              &nbsp;<span class=fa fa-fw fa-external-link aria-hidden=true></span>
            {% elsif parent_sibling.entity.logical_name == 'adx_webfile' %}
              &nbsp;<span class=fa fa-fw fa-file-o aria-hidden=true><span class=sr-only>(File)</span></span>
            {% endif %}
          </a>
        </li>
      {% endif %}
    {% endfor %}
  {% else %}
    <li>
      <ul>
        {% if leaf_mode %}
          {% for parent_sibling in current_page.parent.parent.children %}
            {% if parent_sibling.url == current_page.parent.url %}
              <li>
                <a href={{ current_page.parent.url | h }} title={{ current_page.parent.title | h }}>
                  <span class=fa fa-fw fa-caret-down aria-hidden=true></span>
                  {{ current_page.parent.title | h }}
                </a>
                <ul>
                  {% for sibling in current_page.parent.children %}
                    <li {% if sibling.url == current_page.url %}class=active{% endif %}>
                      <a href={{ sibling.url | h }} title={{ sibling.title | h }}>
                        {% if sibling.children.size > 0 %}
                          <span class=fa fa-fw fa-caret-right aria-hidden=true></span>
                        {% else %}
                          <span class=fa fa-fw aria-hidden=true></span>
                        {% endif %}
                        {{ sibling.title | h }}
                        {% if sibling.entity.logical_name == 'adx_shortcut' %}
                          &nbsp;<span class=fa fa-fw fa-external-link aria-hidden=true></span>
                        {% elsif sibling.entity.logical_name == 'adx_webfile' %}
                          &nbsp;<span class=fa fa-fw fa-file-o aria-hidden=true><span class=sr-only>(File)</span></span>
                        {% endif %}
                      </a>
                    </li>
                  {% endfor %}
                </ul>
              </li>
            {% else %}
              <li>
                <a href={{ parent_sibling.url | h }} title={{ parent_sibling.title | h }}>
                  {% if parent_sibling.children.size > 0 %}
                    <span class=fa fa-fw fa-caret-right aria-hidden=true></span>
                  {% else %}
                    <span class=fa fa-fw aria-hidden=true></span>
                  {% endif %}
                  {{ parent_sibling.title | h }}
                  {% if parent_sibling.entity.logical_name == 'adx_shortcut' %}
                    &nbsp;<span class=fa fa-fw fa-external-link aria-hidden=true></span>
                  {% elsif parent_sibling.entity.logical_name == 'adx_webfile' %}
                    &nbsp;<span class=fa fa-fw fa-file-o aria-hidden=true><span class=sr-only>(File)</span></span>
                  {% endif %}
                </a>
              </li>
            {% endif %}
          {% endfor %}
        {% else %}
          {% for sibling in current_page.parent.children %}
            {% if sibling.url == current_page.url %}
              {{ page_item }}
            {% else %}
              <li>
                <a href={{ sibling.url | h }} title={{ sibling.title | h }}>
                  {% if sibling.children.size > 0 %}
                    <span class=fa fa-fw fa-caret-right aria-hidden=true></span>
                  {% else %}
                    <span class=fa fa-fw aria-hidden=true></span>
                  {% endif %}
                  {{ sibling.title | h }}
                  {% if sibling.entity.logical_name == 'adx_shortcut' %}
                    &nbsp;<span class=fa fa-fw fa-external-link aria-hidden=true></span>
                  {% elsif sibling.entity.logical_name == 'adx_webfile' %}
                    &nbsp;<span class=fa fa-fw fa-file-o aria-hidden=true><span class=sr-only>(File)</span></span>
                  {% endif %}
                </a>
              </li>
            {% endif %}
          {% endfor %}
        {% endif %}
      </ul>
    </li>
  {% endif %}
</ul>

<style type=text/css>
  .side-nav {
    border-right: solid 1px #eee;
  }
  
  .side-nav,
  .side-nav ul {
    list-style: none;
    margin: 0;
    padding: 0;
  }
  
  .side-nav ul {
    margin-left: 20px;
  }
  
  .side-nav a {
    display: block;
    line-height: 30px;
    overflow: hidden;
    text-decoration: none;
    white-space: nowrap;
  }
  
  .side-nav li > a:hover {
    border-right: solid 1px #23527c;
  }
  
  .side-nav li.active > a,
  .side-nav li.active > a:hover {
    border-right: solid 1px #333;
    color: #333;
    font-weight: bold;
  }
</style>
```
### <a name="see-also"></a>Siehe auch

[Erstellen einer benutzerdefinierten Seitenvorlage mithilfe von Liquid und einer Webseiten-Seitenvorlage](create-custom-template.md)  
[Erstellen einer benutzerdefinierte Seitenvorlage zum Rendern eines RSS-Feed](render-rss-custom-page-template.md)  
[Rendern der Entitätsliste, die der aktuellen Seite zugeordnet ist](render-entity-list-current-page.md)  
[Rendern einer Websitekopfzeile und primären Navigationsleiste](render-site-header-primary-navigation.md)  
