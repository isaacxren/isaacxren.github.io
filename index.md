---
layout: without-nav
---

[Isaac Ren](#)
===========
{: title="The 'X' in the URL is my middle initial, Xiaoran :)"}

<div class="card" markdown="1">
![A picture of me with a trombone](me.jpg "This is the current best picture of myself that I have."){:width="240px"}{:height="360"}{:fetchpriority="high"}
<br />
<small>Photo credit: Flora Gaudillière, 2019</small>

*Go to:*
<br />
**home** · [misc](/misc/)

*On this page:*
<br />
[papers](#papers) · [talks](#talks) · [software](#software)

<hr />

| address: | I am currently here<br />But at some point I'll be<br />somewhere else
|---------:|:------------------------------------------------------------------
|   email: | firstlast@kth.se
| twitter: | [@{{ site.twitter.username }}](https://twitter.com/{{ site.twitter.username }})
|  github: | [@{{ site.github.username }}](https://github.com/{{ site.github.username }})

<hr />
</div>

I am a math PhD student at
[KTH Royal Institute of Technology](https://www.kth.se/) in Stockholm, under
the supervision of Associate Professor
[Martina Scolamiero](https://www.kth.se/profile/scola). I also have an
[official profile page](https://www.kth.se/profile/isaacren).

My research interests include topological data analysis and homological
algebra. I have also worked on algebraic rewriting theory and computational
aspects of knot homology.

I have previously studied at École Normale Supérieure de Lyon and Lycée Louis
le Grand. I speak English and French.

{% include to-top.html %}

Preprints & publications {#papers}
------------------------

### Preprints

{% for item in site.data.items.preprints %}
* ["{{ item.title }},"]({{ item.url }}) with {{ item.authors }}, {{ item.year }}. {{ item.comment }}.
{%- endfor %}

### Journal publications

{% for item in site.data.items.papers %}
* ["{{ item.title }},"]({{ item.url }}) with {{ item.authors }}, {{ item.location }}, {{ item.year }}. [arXiv version]({{ item.arxiv }}).
{%- endfor %}

### Conference papers

{% for item in site.data.items.conf %}
* ["{{ item.title }},"]({{ item.url }}) with {{ item.authors }}, {{ item.location }}, {{ item.year }}.
{%- endfor %}

{% include to-top.html %}

Conferences & seminars {#talks}
----------------------

{% for item in site.data.items.talks %}
* "{{ item.title }}," {{""}}
  {%- if item.cospeakers -%}
    with {{ item.cospeakers }}, {{""}}
  {%- endif -%}
  [{{ item.conference }}]({{ item.conf_url }}), {{ item.date }}. {{ item.location }}
  {%- assign first = true -%}
  {%- if item.slides or item.video %}: {% endif -%}
  {%- if item.slides -%}
    {%- if first != true %}, {% endif -%}
    [slides]({{ item.slides }})
    {%- assign first = false -%}
  {%- endif -%}
  {%- if item.video -%}
    {%- if first != true %}, {% endif -%}
    [video]({{ item.video }})
    {%- assign first = false -%}
  {%- endif -%}
  {%- for subitem in item.related -%}
    {%- if subitem.slides -%}
      {%- if first != true %}, {% endif -%}
      [slides]({{ subitem.slides }})
      {%- assign first = false -%}
    {%- endif -%}
    {%- if subitem.video -%}
      {%- if first != true %}, {% endif -%}
      [video]({{ subitem.video }})
      {%- assign first = false -%}
    {%- endif -%}
    {{""}} from a similar talk at [{{ subitem.conference }}]({{ subitem.conf_url }})
  {%- endfor -%}
  .
{%- endfor %}

{% include to-top.html %}

Software {#software}
--------

{% for item in site.data.items.software %}
* [***{{ item.title }}***]({{ item.url }}), {{ item.description }}.
{%- endfor %}