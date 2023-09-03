---
date: 2023-08-19
share: true
title: Theme
parent: WebPage
---
# Theme
---

Na stronie wykorzystuję szablon: [Just the Docs (just-the-docs.com)](https://just-the-docs.com)

### MathJax
---
Dodanie wsparcia dla mathjax w `_config.yaml` strony. Kolejne linie odpowiadają za dodanie adresu skryptu do MathJax w wersji 3 oraz konfiguracji MathJaxa'a. Wyłączenia compresji html, oraz wyłączenia przetwarzania bloków matematyki w parserze Markwowna.
```yaml
mathjax:
  source: https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js
  config: 'window.MathJax = {tex: {packages: ["base", "ams"], inlineMath: ["$", "$"](%22$%22,%20%22$%22.md), displayMath: ["$", "$"](%22$%22,%20%22$%22.md) }}'

compress_html:
  blanklines: true

kramdown:
  math-engine: nil
```

Aby włączyc MathJax trzeba dodać poniżesze do pliku `_includes/head_custom.html`

```html
{% if page.mathjax %}
  <script type="text/javascript">
    {{ site.mathjax.config }};
  </script>
  <script type="text/javascript" id="MathJax-script" async 
    src="{{ site.mathjax.source }}">
  </script>
{% endif %}
```

Wtedy na stronach które mają dodany parametr do yaml
```yaml
mathjax: true
```
renderowaną są wzory

Z jakiegoś powodu podczas eksportu przez [GithubPublisher](GithubPublisher.md) z Obsidiana bloki matematyki oznaczone za pomocą `$$` są konwertowane do `\( ... \)`. Aby poprawnie wyświetlac wzory w konfiguracji MathJaxa dodałem parsowanie znaków `\( ... \)`.