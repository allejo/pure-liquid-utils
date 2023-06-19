# Pure Liquid Utilities

Pure Liquid Utilities (PLUtils) is a repo where I can store shared utilities between my [Pure Liquid projects](http://pure-liquid.allejo.org).

## `pltest.py`

A Python 3 script used for checking Jekyll assertions; ensuring that the expected HTML is generated from given Liquid. In a Liquid project, set up a collection so that you can create different items in that collection that each will render different behaviors of your Liquid snippet.

```yaml
# _config.yml

theme: null

collections:
  tests:
    output: true

defaults:
  - scope:
      path: ""
      type: tests
    values:
      layout: null
      permalink: /tests/:name
```

Each item in the test collection should have two sections separated by the `<!-- /// -->` directive. The top section will be the Liquid you need to write and the bottom section contains the HTML that is expected to be generated.

```html
---
---

{% capture markdown %}
# Heading 1
{% endcapture %}
{% assign text = markdown | markdownify %}

{% include anchor_headings.html html=text anchorAttrs='aria-label="Link to &quot;%heading%&quot;"' %}

<!-- /// -->

<h1 id="heading-1">Heading 1 <a href="#heading-1" aria-label="Link to &quot;Heading 1&quot;"></a></h1>
```

> **Warning**
> The expected output (the bottom section), can only contain **ONE** HTML element. If you need to have multiple HTML elements, wrap everything with a `<div>` (this is very React-esque).
