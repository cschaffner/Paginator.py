# Paginator

Paginator for SQLAlchemy query object, list or iterable

---

## Install

    pip install paginator

### Simple Usage with an iterable

    from paginator import Paginator

    items = range(1, 1000)
    
    items = Paginator(items, page=1, per_page=10)
    
    for item in items:
        pass
    
### Jinja macro
 
 
    {% macro pagination(paginator, endpoint=None, class_='pagination') %}
        {% if not endpoint %}
            {% set endpoint = request.endpoint %}
        {% endif %}
        {% if "page" in kwargs %}
            {% do kwargs.pop("page") %}
        {% endif %}
        <nav>
            <ul class="{{ class_ }}">
              {%- if paginator.has_prev %}
                <li><a href="{{ url_for(endpoint, page=paginator.prev_page_number, **kwargs) }}"
                 rel="me prev"><span aria-hidden="true">&laquo;</span></a></li>
              {% else %}
                <li class="disabled"><span><span aria-hidden="true">&laquo;</span></span></li>
              {%- endif %}
    
              {%- for page in paginator.pages %}
                {% if page %}
                  {% if page != paginator.page %}
                    <li><a href="{{ url_for(endpoint, page=page, **kwargs) }}"
                     rel="me">{{ page }}</a></li>
                  {% else %}
                    <li class="active"><span>{{ page }}</span></li>
                  {% endif %}
                {% else %}
                  <li><span class=ellipsis>…</span></li>
                {% endif %}
              {%- endfor %}
    
              {%- if paginator.has_next %}
                <li><a href="{{ url_for(endpoint, page=paginator.next_page_number, **kwargs) }}"
                 rel="me next">»</a></li>
              {% else %}
                <li class="disabled"><span aria-hidden="true">&raquo;</span></li>
              {%- endif %}
            </ul>
        </nav>
    {% endmacro %}

    
### DOCUMENTATION IN CONSTRUCTION

---

(c) 2015 Mardix

