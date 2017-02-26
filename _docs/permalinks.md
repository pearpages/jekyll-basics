# Permalinks

You construct permalinks by creating a template URL where dynamic elements are represented by colon-prefixed keywords. Each of the colon-prefixed keywords is a template variable.

## Default pattern

The default template permalink is ```/:categories/:year/:month/:day/:title.html```.

This is the equivalent of:

```
permalink: date
```

## Where to configure permalinks

You can configure your site’s permalinks through the Configuration file or in the Front Matter for each post, page, or collection.

## Template variables for permalinks

- year
- month
_ i_month
- day
- i_day
- short_year
- hour
- minute
- second
- title
- slug (slugified title from the document's filename)
- categories
