# Data Files

Jekyll supports loading data from **YAML**, **JSON**, and **CSV** files located in the _data directory. 

> Note that CSV files must contain a header row.

## Example: Accessing a specific authorPermalinkPermalink

Pages and posts can also access a specific data item. The example below shows how to access a specific item:

_data/people.yml:

```yml
dave:
    name: David Smith
    twitter: DavidSilvaSmith
The author can then be specified as a page variable in a post’s frontmatter:
```

```yml
---
title: sample post
author: dave
---

{% assign author = site.data.people[page.author] %}
<a rel="author"
  href="https://twitter.com/{{ author.twitter }}"
  title="{{ author.name }}">
    {{ author.name }}
</a>
```
