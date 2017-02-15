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

## Default Configuration

```yml
# Where things are
source:       .
destination:  ./_site
plugins_dir:  _plugins
layouts_dir:  _layouts
data_dir:     _data
includes_dir: _includes
collections:
  posts:
    output:   true

# Handling Reading
safe:         false
include:      [".htaccess"]
exclude:      ["node_modules", "vendor/bundle/", "vendor/cache/", "vendor/gems/", "vendor/ruby/"]
keep_files:   [".git", ".svn"]
encoding:     "utf-8"
markdown_ext: "markdown,mkdown,mkdn,mkd,md"

# Filtering Content
show_drafts: null
limit_posts: 0
future:      false
unpublished: false

# Plugins
whitelist: []
gems:      []

# Conversion
markdown:    kramdown
highlighter: rouge
lsi:         false
excerpt_separator: "\n\n"
incremental: false

# Serving
detach:  false
port:    4000
host:    127.0.0.1
baseurl: "" # does not include hostname
show_dir_listing: false

# Outputting
permalink:     date
paginate_path: /page:num
timezone:      null

quiet:    false
verbose:  false
defaults: []

liquid:
  error_mode: warn

# Markdown Processors
rdiscount:
  extensions: []

redcarpet:
  extensions: []

kramdown:
  auto_ids:       true
  footnote_nr:    1
  entity_output:  as_char
  toc_levels:     1..6
  smart_quotes:   lsquo,rsquo,ldquo,rdquo
  input:          GFM
  hard_wrap:      false
  footnote_nr:    1
```