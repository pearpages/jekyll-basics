# Jekyll Tips

+ Liquid template system

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