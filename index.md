---
layout: without-nav
title: Isaac Ren
---

<div class="card" markdown="1">
![A picture of me with a trombone](/s/photo.jpg "This is the current best picture of myself that I have."){:width="240px"}{:height="360"}{:fetchpriority="high"}
<br />
<small>Photo credit: Flora Gaudillière, 2019</small>

*Go to:*
<br />
{% include nav.html %}

*On this page:*
<br />
[papers](#papers) · [talks](#talks) · [software](#software)

<hr />

| address: | {% include hidden-message.html text="I am currently here<br />But at some point I'll be<br />somewhere else" message="This is actually just an attempt at a haiku :)" %}{: style="white-space: nowrap;"}
|   email: | firstlast@kth.se
| twitter: | [@{{ site.twitter.username }}](https://twitter.com/{{ site.twitter.username }})
|  github: | [@{{ site.github.username }}](https://github.com/{{ site.github.username }})

<hr />
</div>

I am soon to be a math postdoctoral researcher at
[Imperial College London](https://www.imperial.ac.uk/), under the mentorship of
[Anthea Monod](https://sites.google.com/view/antheamonod/) and funded by the
[Knut and Alice Wallenberg Foundation](https://kaw.wallenberg.org/en/knut-and-alice-wallenberg-foundation)
and [WASP](https://wasp-sweden.org/wasp-postdoc/).

I obtained my PhD at
[KTH Royal Institute of Technology](https://www.kth.se/) in Stockholm, under
the supervision of Associate Professor
[Martina Scolamiero](https://www.kth.se/profile/scola) and Professor
[Wojciech Chachólski](https://www.kth.se/profile/wojtek?l=en).

My research interests include topological data analysis and homological
algebra. I have also worked on algebraic rewriting theory and computational
aspects of knot homology.

I have previously studied at École Normale Supérieure de Lyon and Lycée Louis
le Grand. I speak English and French.

[~ ˆ ~](# "Top of the page"){:.to-top}

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

### Thesis

I defended my thesis
["Algebraic invariants for filtered spaces and their computation"](thesis.pdf){:.file-size data-size="4.4 MB"}
on May 29th, 2026. The published version of my thesis is available
[on DiVA](https://urn.kb.se/resolve?urn=urn:nbn:se:kth:diva-380673), and the
source material is available
[on GitHub](https://github.com/th-rtyf-re/phd-thesis).

[~ ˆ ~](# "Top of the page"){:.to-top}

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

[~ ˆ ~](# "Top of the page"){:.to-top}

Software {#software}
--------

{% for item in site.data.items.software %}
* [***{{ item.title }}***]({{ item.url }}), {{ item.description }}.
{%- endfor %}