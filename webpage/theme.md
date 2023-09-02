---
date: 2023-08-19
share: true
title: Theme
parent: WebPage
---
# Theme
---

Na stronie wykorzystuję szablon: [Just the Docs (just-the-docs.com)](https://just-the-docs.com)

Test2

test3

### MathJax
---
Dodanie wsparcia dla mathjax w `_config.yaml` strony
```yaml
mathjax:
  source: https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/latest.js?config=TeX-AMS_CHTML
  config: 'MathJax.Hub.Config({ TeX: { equationNumbers: { autoNumber: "AMS" } }, tex2jax: { inlineMath: [' } })'

compress_html:
  blanklines: true
```

Aby włączyc MathJax trzeba dodać poniżesze do pliku `_includes/head_custom.html`

```html
{% if page.mathjax %}
  <script type="text/x-mathjax-config">
    {{ site.mathjax.config }};
  </script>
  <script type="text/javascript" async 
    src="{{ site.mathjax.source }}">
  </script>
{% endif %}
```

Wtedy na stronach które mają dodany parametr do yaml
```yaml
mathjax: true
```
renderowaną są wzory,' } })'

compress_html:
  blanklines: true
```

Aby włączyc MathJax trzeba dodać poniżesze do pliku `_includes/head_custom.html`

```html
{% if page.mathjax %}
  <script type="text/x-mathjax-config">
    {{ site.mathjax.config }};
  </script>
  <script type="text/javascript" async 
    src="{{ site.mathjax.source }}">
  </script>
{% endif %}
```

Wtedy na stronach które mają dodany parametr do yaml
```yaml
mathjax: true
```
renderowaną są wzory](' } })'

compress_html:
  blanklines: true
```

Aby włączyc MathJax trzeba dodać poniżesze do pliku `_includes/head_custom.html`

```html
{% if page.mathjax %}
  <script type="text/x-mathjax-config">
    {{ site.mathjax.config }};
  </script>
  <script type="text/javascript" async 
    src="{{ site.mathjax.source }}">
  </script>
{% endif %}
```

Wtedy na stronach które mają dodany parametr do yaml
```yaml
mathjax: true
```
renderowaną są wzory,' } })'

compress_html:
  blanklines: true
```

Aby włączyc MathJax trzeba dodać poniżesze do pliku `_includes/head_custom.html`

```html
{% if page.mathjax %}
  <script type="text/x-mathjax-config">
    {{ site.mathjax.config }};
  </script>
  <script type="text/javascript" async 
    src="{{ site.mathjax.source }}">
  </script>
{% endif %}
```

Wtedy na stronach które mają dodany parametr do yaml
```yaml
mathjax: true
```
renderowaną są wzory.md) } })'

compress_html:
  blanklines: true
```

Aby włączyc MathJax trzeba dodać poniżesze do pliku `_includes/head_custom.html`

```html
{% if page.mathjax %}
  <script type="text/x-mathjax-config">
    {{ site.mathjax.config }};
  </script>
  <script type="text/javascript" async 
    src="{{ site.mathjax.source }}">
  </script>
{% endif %}
```

Wtedy na stronach które mają dodany parametr do yaml
```yaml
mathjax: true
```
renderowaną są wzory