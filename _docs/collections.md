# Collections

 Collections allow you to define a new type of document that behave like Pages or Posts do normally, but also have their own unique properties and namespace.

## Setup

1. Step 1: Tell Jekyll to read in your collection
2. Step 2: Add your content
3. Step 3: Optionally render your collection’s documents into independent files

### 1. Tell Jekyll to read in your collection

```yaml
collections:
  my_collection
```

```yaml
collections:
  speakers:
    output: true
  events:
    output: true
```

You can optionally specify metadata for your collection in the configuration:

```yaml
collections:
  my_collection:
    foo: bar
```

Default attributes can also be set for a collection:

```yaml
defaults:
  - scope:
      path: ""
      type: my_collection
    values:
      layout: page
```

### 2. Add your content

Create a corresponding folder (e.g. ```<source>/_my_collection```) and add documents. 

> If no YAML front matter is provided, Jekyll will not generate the file in your collection.

> The folder must be named identically to the collection you defined in your _config.yml file, with the addition of the preceding _ character.

### 3. Optionally render your collection’s documents into independent files

If you’d like Jekyll to create a public-facing, rendered version of each document in your collection, set the output key to true in your collection metadata in your **_config.yml**:

```
collections:
  my_collection:
    output: true
```

This will produce a file for each document in the collection. For example, if you have ```_my_collection/some_subdir/some_doc.md```, it will be rendered using Liquid and the Markdown converter of your choice and written out to ```<dest>/my_collection/some_subdir/some_doc.html```.

---

## Permalinks

```yaml
collections:
- my_collection:
    output: true
    permalink: /awesome/:path/:title.:output_ext
```

Collections have the following template variables available for permalinks:

+ collection *Label of the containing collection.*
+ path *Path to the document relative to the collection's directory.*
+ name *The document's base filename, with every sequence of spaces and non-alphanumeric characters replaced by a hyphen.*
+ title *The document's lowercase title (as defined in its front matter), with every sequence of spaces and non-alphanumeric characters replaced by a hyphen. If the document does not define a title in its front matter, this is equivalent to name.*
+ output_ext *Extension of the output file.*

### example

Let’s say your collection is called apidocs with doc1.md in your collection. doc1.md is grouped inside a folder called **mydocs**. Your project’s source directory for the collection looks this:

```
├── \_apidocs
│   └── mydocs
│       └── doc1.md
```
Based on this scenario, here are a few permalink options.

#### Permalink configuration 1: [Nothing configured] 

Output:

```
├── apidocs
│   └── mydocs
│       └── doc1.html
```

#### Permalink configuration 2: /:collection/:path/:title:output_ext 

Output:

```
├── apidocs
│   └── mydocs
│       └── doc1.html
```

#### Permalink configuration 3: No collection permalinks configured, but pretty configured for pages/posts. 

Output:

```
├── apidocs
│   └── mydocs
│       └── doc1
│           └── index.html
```

#### Permalink configuration 4: /awesome/:path/:title.html 

Output:

```
├── awesome
│   └── mydocs
│       └── doc1.html
```

#### Permalink configuration 5: /awesome/:path/:title/ 

Output:

```
├── awesome
│   └── mydocs
│       └── doc1
│           └── index.html
```

#### Permalink configuration 6: /awesome/:title.html 

Output:

```
├── awesome
│   └── doc1.html
```

#### Permalink configuration 7: :title.html Output:

```
├── doc1.html
```

---

## Liquid attributes

### Accessing a Collection

Each collection is accessible as a field on the site variable. For example, if you want to access the albums collection found in **_albums**, you’d use **site.albums**.

Each collection is itself an array of documents (e.g., site.albums is an array of documents, much like site.pages and site.posts).

### Accessing All Collections

The collections are also available under ```site.collections```, with the metadata you specified in your **_config.yml**.

+ label *The name of your collection, e.g. my_collection.*
+ docs *An array of documents.*
+ files *An array of static files in the collection.*
+ relative_directory *The path to the collection's source directory, relative to the site source.*
+ directory *The full path to the collections's source directory.*
+ output *Whether the collection's documents will be output as individual files. *

Example in template

```html
{% for c in site.collections %}
    {{c.label}} {{c.relative_directory}} {{c.directory}} {{c.output}} {{c.meta_var}}
{% endfor %}
```

### Accessing a Collection (Documents)

In addition to any YAML *Front Matter* provided in the document’s corresponding file, each document has the following attributes:

+ content *The (unrendered) content of the document. If no YAML Front Matter is provided, Jekyll will not generate the file in your collection. If YAML Front Matter is used, then this is all the contents of the file after the terminating `---` of the front matter.*
+ output *The rendered output of the document, based on the  content.*
+ path *The full path to the document's source file.*
+ relative_path *The path to the document's source file relative to the site source.*
+ url *The URL of the rendered collection. The file is only written to the destination when the collection to which it belongs has output: true in the site's configuration.*
+ collection *The name of the document's collection.*
+ date *The date of the document's collection.*

### Accessing Collection attributes

Attributes from the YAML front matter can be accessed as data anywhere in the site. 

You might have front matter in an individual file structured as follows (which must use a supported markup format, and cannot be saved with a .yaml extension):

```yaml
title: "Josquin: Missa De beata virgine and Missa Ave maris stella"
artist: "The Tallis Scholars"
director: "Peter Phillips"
works:
  - title: "Missa De beata virgine"
    composer: "Josquin des Prez"
    tracks:
      - title: "Kyrie"
        duration: "4:25"
      - title: "Gloria"
        duration: "9:53"
      - title: "Credo"
        duration: "9:09"
      - title: "Sanctus & Benedictus"
        duration: "7:47"
      - title: "Agnus Dei I, II & III"
        duration: "6:49"
```

Every album in the collection could be listed on a single page with a template:

```html
{% for album in site.albums %}
  <h2>{{ album.title }}</h2>
  <p>Performed by {{ album.artist }}{% if album.director %}, directed by {{ album.director }}{% endif %}</p>
  {% for work in album.works %}
    <h3>{{ work.title }}</h3>
    <p>Composed by {{ work.composer }}</p>
    <ul>
    {% for track in work.tracks %}
      <li>{{ track.title }} ({{ track.duration }})</li>
    {% endfor %}
    </ul>
  {% endfor %}
{% endfor %}
```
