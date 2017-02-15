# Jekyll Tips

## Pending Topics

+ Liquid template system

---

## Basic Usage

> Changes to _config.yml are not included during automatic regeneration.

### Defining Source and Destination Folders in Config File

```yaml
source:      _source
destination: _deploy
```

Then the following two commands will be equivalent:

```
$ jekyll build
$ jekyll build --source _source --destination _deploy
```

---

## Blog Migrations

[Jekyll Import Docs Site](https://import.jekyllrb.com/docs/home/)

---

## Sass

### Files

Accepts the extensions ```.sass, .scss```.

with two lines of triple dashes, like this:

```sass
---
---

// start content
.my-definition
  font-size: 1.2em
```

### Output

The output file will be placed in the same directory that it came from. For instance, if you have a file named **css/styles.scss** in your site’s source folder, Jekyll will process it and put it in your site’s destination folder under **css/styles.css**.

### Folders

#### Partials

Partials must go in the default ```_sass``` folder.

 Place your **main** SCSS or Sass files in the place you want them to be in the output file, such as <source>/css. 

 ### _config.yml

 ```yaml
 sass:
    sass_dir: _sass #partials, folder by default, not need to write it
    style: compressed
 ```

 ---