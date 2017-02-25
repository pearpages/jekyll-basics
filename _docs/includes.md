# Includes

The **include** tag allows you to include the content from another file stored in the **_includes** folder:

```liquid
{% include footer.html %}
```

Jekyll will look for the reference file (in this case, **footer.html**) in the **_includes** directory at the root of your source directory and insert its contents.

## Including files relative to another file

You can choose to include file fragments relative to the current file by using the **include_relative** tag:

```liquid
{% include_relative somedir/footer.html %}
```

**You won't need to palce your included content within *includes* directory**. Instead, the inclusion is specifically relative to the file where the tag is being used.

> Note that you cannot use the ../ syntax to specify an include location that refers to a higher-level directory.

## Using variables names for the include file

The name of the file you want to embed can be specified as a variable instead of an actual file name. For example, suppose you defined a variable in your page’s front matter like this:

```yaml
---
title: My page
my_variable: footer_company_a.html
---
```

You could then reference that variable include:

```html
{% include {{page.my_variable}} %}
```

## Passing parameters to includes

You can pass parameters to an include.

```html
<div markdown="span" class="alert alert-info" role="alert">
<i class="fa fa-info-circle"></i> <b>Note:</b>
{{ include.content }}
</div>
```

The *include.content* parameter comes from

```html
{% include note.html content="This is my sample note." %} 
```

### Default filter

```html
Dear {{ customer.name | default: "customer" }}
```

