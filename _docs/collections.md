 # Collections

 Collections allow you to define a new type of document that behave like Pages or Posts do normally, but also have their own unique properties and namespace.

## Setup

1. Step 1: Tell Jekyll to read in your collection
2. Step 2: Add your content
3. Step 3: Optionally render your collection’s documents into independent files

### 1. Tell Jekyll to read in your collection

```yaml
collections:
- my_collection
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

