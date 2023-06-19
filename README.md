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

Each item in the test collection should have two sections separated by the `<!-- /// -->` directive. The top section will be the Liquid you need to write and the bottom section contains the HTML that is expected to be generated. Use the Front Matter section to write any notes for that test; e.g. what issue are you adding this unit test because of.

```html
---
# See: https://github.com/allejo/jekyll-anchor-headings/issues/38
---

{% capture text %}
<div>
  <h2 data-ignore-me="">Hello world</h2>
  <h2 data-ignore-me="">Greetings world</h2>
  <h2 data-ignore-me="">Sup world</h2>
  <h2 data-ignore-me="">Yo world</h2>
</div>
{% endcapture %}

{% include anchor_headings.html html=text generateId=true %}

<!-- /// -->

<div>
  <h2 data-ignore-me="" id="hello-world">Hello world <a href="#hello-world"></a></h2>
  <h2 data-ignore-me="" id="greetings-world">Greetings world <a href="#greetings-world"></a></h2>
  <h2 data-ignore-me="" id="sup-world">Sup world <a href="#sup-world"></a></h2>
  <h2 data-ignore-me="" id="yo-world">Yo world <a href="#yo-world"></a></h2>
</div>
```

> **Warning**
>
> The expected output (the bottom section), can only contain **ONE** HTML element. If you need to have multiple HTML elements, wrap everything with a `<div>` (this is very React-esque).
