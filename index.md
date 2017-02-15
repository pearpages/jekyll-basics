---
# You don't need to edit this file, it's empty on purpose.
# Edit theme's home layout instead if you wanna make some changes
# See: https://jekyllrb.com/docs/themes/#overriding-theme-defaults
layout: home
---

## Site title var 

{{ site.title }}

---

## Collections

{% for c in site.collections %}
    {{c.label}} {{c.relative_directory}} {{c.directory}} {{c.output}} {{c.happy}}
{% endfor %}

---

## Speaker Collections

{% for speaker in site.speakers %}
    {{speaker.title}}
{% endfor %}

### Accessing One Specific Element From the Array

{{ site.speakers[0] }}

{{ site.speakers | first}}

{{ site.speakers | last}}

{{ site.speakers | where: "title","Pere Pages"}}

---

