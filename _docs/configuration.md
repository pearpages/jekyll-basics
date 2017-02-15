# Configuration _config.yml

## Global Configuration

+ source: DIR
+ destination: DIR
+ safe: BOOL *Disable custom plugins, and ignore symbolic links.*
+ exclude: [DIR, FILE, ...]
+ include: [DIR, FILE, ...] (.e.g. .htaccess)
+ keep_files: [DIR, FILE, ...]
+ timezone: TIMEZONE
+ encoding: ENCODING
+ defaults: *Set defaults for YAML Front Matter variables.*

## Build Command Options

+ show_drafts: BOOL
+ future: BOOL
+ unpublished: BOOL
+ lsi: BOOL
+ limit_posts: NUM
+ incremental: BOOL
+ profile: BOOL

## Serve Options

+ port: PORT
+ host: HOSTNAME
+ baseurl: URL
+ detach: BOOL

## Custom WEBrick Headers

You can provide custom headers for your site by adding them to _config.yml

```yml
# File: _config.yml
webrick:
  headers:
    My-Header: My-Value
    My-Other-Header: My-Other-Value
```

### Defaults

We provide by default **Content-Type** and **Cache-Control** response headers.

## Front Matter defaults

```yml
defaults:
  -
    scope:
      path: "" # an empty string here means all files in the project
    values:
      layout: "default"
```

```yml
defaults:
  -
    scope:
      path: ""
      type: "posts"
    values:
      layout: "my-site"
  -
    scope:
      path: "projects"
      type: "pages" # previously `page` in Jekyll 2.2.
    values:
      layout: "project" # overrides previous default layout
      author: "Mr. Hyde"
```

```yml
collections:
  my_collection:
    output: true

defaults:
  -
    scope:
      path: ""
      type: "my_collection" # a collection in your site, in plural form
    values:
      layout: "default"
```