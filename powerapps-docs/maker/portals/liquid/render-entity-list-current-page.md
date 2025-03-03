---
title: Darstellen der Entitätsliste, die der aktuellen Seite in einem Portal zugeordnet ist | MicrosoftDocs
description: Beispielcode zum Rendern der Entitätsliste, die der aktuellen Seite in einem Portal zugeordnet ist.
author: sbmjais
manager: shujoshi
ms.service: powerapps
ms.topic: conceptual
ms.custom: ''
ms.date: 10/07/2019
ms.author: shjais
ms.reviewer: ''
ms.openlocfilehash: e31f83efb7cedfa42b6c4c9e7da83280b261d9c8
ms.sourcegitcommit: 8185f87dddf05ee256491feab9873e9143535e02
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/01/2019
ms.locfileid: "2707953"
---
# <a name="render-the-entity-list-associated-with-the-current-page"></a>Rendern der Entitätsliste, die der aktuellen Seite zugeordnet ist

Rendern der Entitätsliste, die der aktuellen Seite zugeordnet ist, als sortierbare Tabelle mit Seitennummerierung. Verwendet [entitylist](liquid-objects.md#entitylist), [entitylist](liquid-objects.md#entityview), [PowerApps Common Data Service Entity-Tags](portals-entity-tags.md), [Site](liquid-objects.md#page) und [Query](liquid-objects.md#request) Parameter, einschließlich Suche und Auswahl mehrerer Ansichten.  

```xml
{% entitylist id:page.adx_entitylist.id %}
  <div class="navbar navbar-default">
    <div class="container-fluid">
      <div class="navbar-header">
        <button type="button" class="navbar-toggle"
          data-toggle="collapse"
          data-target="#entitylist-navbar-{{ entitylist.id }}">
          <span class="sr-only">Toggle navigation</span>
          <span class="icon-bar"></span>
          <span class="icon-bar"></span>
          <span class="icon-bar"></span>
        </button>
        <a class="navbar-brand" href="{{ page.url }}">{{ entitylist.adx_name }}</a>
      </div>
      <div class="collapse navbar-collapse" id="entitylist-navbar-{{ entitylist.id }}">

        {% if entitylist.views.size > 1 %}
          <ul class="nav navbar-nav">
            <li class="dropdown">
              <a href="#" class="dropdown-toggle" data-toggle="dropdown">
                <i class="fa fa-list"></i> Views <span class="caret"></span>
              </a>
              <ul class="dropdown-menu" role="menu">
                {% for view in entitylist.views -%}
                  <li{% if params.view == view.id %} class="active"{% endif %}>
                    <a href="{{ request.path | add_query:'view', view.id }}">{{view.name}}</a>
                  </li>
                {% endfor -%}
              </ul>
            </li>
          </ul>
        {% endif %}
      
        {% if entitylist.search_enabled %}
          <form class="navbar-form navbar-left" method="get">
            <div class="input-group">
              {% if params.search.size > 0 %}
                <div class="input-group-btn">
                  <a class="btn btn-default"
                    href="{{ request.path_and_query | remove_query:'search' }}">&times;</a>
                </div>
              {% endif %}
              <input name="search" class="form-control"
                value="{{ params.search }}"
                placeholder="{{ entitylist.search_placeholder | default: 'Search' }}"
                type="text" />
              <div class="input-group-btn">
                <button type="submit" class="btn btn-default"
                  title="{{ entitylist.search_tooltip }}">
                  <i class="fa fa-search">&nbsp;</i>
                </button>
              </div>
            </div>
          </form>
        {% endif %}
        
        {% if entitylist.create_enabled %}
          <ul class="nav navbar-nav navbar-right">
            <li>
              <a href="{{ entitylist.create_url }}">
                <i class="fa fa-plus"></i> {{ entitylist.create_label | default: 'Create' }}
              </a>
            </li>
          </ul>
        {% endif %}
        
      </div>
    </div>
  </div>
  
  {% entityview id:params.view, search:params.search, order:params.order, page:params.page, pagesize:params.pagesize, metafilter:params.mf %}
    {% assign order = params.order | default: entityview.sort_expression %}
    <table class="table" data-order="{{ order }}">
      <thead>
        <tr>
          {% for c in entityview.columns -%}
            <th width="{{ c.width }}" data-logicalname="{{ c.logical_name }}">
              {% if c.sort_enabled %}
                {% assign current_sort = order | current_sort:c.logical_name %}
                {% case current_sort %}
                {% when 'ASC' %}
                  <a href="{{ request.path_and_query | add_query:'order', c.sort_descending }}">
                    {{ c.name }} <i class="fa fa-sort-asc"></i>
                  </a>
                {% when 'DESC' %}
                  <a href="{{ request.path_and_query | add_query:'order', c.sort_ascending }}">
                    {{ c.name }} <i class="fa fa-sort-desc"></i>
                  </a>
                {% else %}
                  <a href="{{ request.path_and_query | add_query:'order', c.sort_ascending }}">
                    {{ c.name }} <i class="fa fa-unsorted"></i>
                  </a>
                {% endcase %}
              {% else %}
                {{ c.name }}
              {% endif %}
            </th>
          {% endfor -%}
          <th width="1"></th>
        </tr>
      </thead>

      <tbody>
        {% for e in entityview.records -%}
          <tr>

            {% for c in entityview.columns -%}
              {% assign attr = e[c.logical_name] %}
              {% assign attr_type = c.attribute_type | downcase %}

              <td data-logicalname="{{ c.logical_name }}">
                {% if attr.is_entity_reference -%}
                  {{ attr.name }}
                {% elsif attr_type == 'datetime' %}
                  {% if attr %}
                    <time datetime="{{ attr | date_to_iso8601 }}">
                      {{ attr }}
                    </time>
                  {% endif %}
                {% elsif attr_type == 'picklist' %}
                  {{ attr.label }}
                {% else %}
                  {{ attr }}
                {% endif -%}
              </th>
            {% endfor -%}

            <td>
              {% if entitylist.detail_enabled -%}
                <a class="btn btn-default btn-xs"
                  href="{{ entitylist.detail_url}}?{{ entitylist.detail_id_parameter }}={{ e.id }}"
                  title="{{ entitylist.detail_label }}">
                  <i class="fa fa-external-link"></i>
                </a>
              {% endif -%}
            </td>

          <tr>
        {% endfor -%}
      </tbody>
    </table>
    
    {% if entityview.pages.size > 0 %}
      {% assign first_page = entityview.first_page %}
      {% assign last_page = entityview.last_page %}
      {% assign page_offset = entityview.page | minus:1 | divided_by:10 | times:10 %}
      {% assign page_slice_first_page = page_offset | plus:1 %}
      {% assign page_slice_last_page = page_offset | plus:10 %}

      <ul class="pagination">
        <li {% unless first_page and entityview.page > 1 %}class="disabled"{% endunless %}>
          <a
            {% if first_page and entityview.page > 1 %}
              href="{{ request.url | add_query:'page', first_page | path_and_query }}"
            {% endif %}>
            &laquo;
          </a>
        </li>

        <li {% unless entityview.previous_page %}class="disabled"{% endunless %}>
          <a
            {% if entityview.previous_page %}
              href="{{ request.url | add_query:'page', entityview.previous_page | path_and_query }}"
            {% endif %}>
            &lsaquo;
          </a>
        </li>

        {% if page_slice_first_page > 1 %}
          {% assign previous_slice_last_page = page_slice_first_page | minus:1 %}
          <li>
            <a href="{{ request.url | add_query:'page', previous_slice_last_page | path_and_query }}">
              &hellip;
            </a>
          </li>
        {% endif %}

        {% for page in entityview.pages offset:page_offset limit:10 -%}
          <li{% if page == entityview.page %} class="active"{% endif %}>
            <a href="{{ request.url | add_query:'page', page | path_and_query }}">
              {{ page }}
            </a>
          </li>
        {% endfor -%}

        {% if page_slice_last_page < entityview.pages.size %}
          {% assign next_slice_first_page = page_slice_last_page | plus:1 %}
          <li>
            <a href="{{ request.url | add_query:'page', next_slice_first_page | path_and_query }}">
              &hellip;
            </a>
          </li>
        {% endif %}

        <li {% unless entityview.next_page %}class="disabled"{% endunless %}>
          <a
            {% if entityview.next_page %}
              href="{{ request.url | add_query:'page', entityview.next_page | path_and_query }}"
            {% endif %}>
            &rsaquo;
          </a>
        </li>

        <li {% unless last_page and entityview.page < last_page %}class="disabled"{% endunless %}>
          <a
            {% if last_page and entityview.page < last_page %}
              href="{{ request.url | add_query:'page', last_page | path_and_query }}"
            {% endif %}>
            &raquo;
          </a>
        </li>
      </ul>

    {% endif %}
    
  {% endentityview %}
{% endentitylist %}
```

### <a name="see-also"></a>Siehe auch

[Erstellen einer benutzerdefinierten Seitenvorlage mithilfe von Liquid und einer Webseiten-Seitenvorlage](create-custom-template.md)  
[Erstellen einer benutzerdefinierte Seitenvorlage zum Rendern eines RSS-Feed](render-rss-custom-page-template.md)  
[Rendern einer Websitekopfzeile und primären Navigationsleiste](render-site-header-primary-navigation.md)  
[Rendern von bis zu drei Ebenen der Seitenhierarchie mithilfe der hybriden Navigation](hybrid-navigation-render-page-hierachy.md)
