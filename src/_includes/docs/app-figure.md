{% assign alt = include.alt | default: include.caption -%}
{% assign caption = include.caption | default: include.platform -%}
{% if include.width -%}
{% assign width = 'width: ' | append: include.width | append: ';' -%}
{% else -%}
{% assign width = '' -%}
{% endif -%}
{% if include.height -%}
{% assign height = 'height: ' | append: include.height | append: ';' -%}
{% else -%}
{% assign height = '' -%}
{% endif -%}

{% comment %}
NOTE possibly sneaky introspection, feeling like this should be removed
NOTE(rearch) We second that, never a good idea.
{% endcomment %}
{% if include.path-prefix -%}
  {% assign path = include.path-prefix | append: '/' -%}
{% else -%}
  {% assign path = '' -%}
{% endif -%}

{% if include.platform -%}
  {% assign alt = alt | append: ' on ' | append: include.platform -%}
  {% assign platform_in_lowercase = include.platform | downcase -%}
  {% assign path = path | append: platform_in_lowercase | append: '/'  -%}
{% endif -%}

<figure class="site-figure {{include.class}}">
  <div class="site-figure-container">
    <img src='/assets/images/docs/{{path}}{{include.image}}'
         class='{{include.img-class}}'
         alt='{{alt}}'
         style='{{width}} {{height}}'
         >
    {% if caption -%}
      <figcaption class="figure-caption">{{caption}}</figcaption>
    {% endif -%}
  </div>
</figure>
