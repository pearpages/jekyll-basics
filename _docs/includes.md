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