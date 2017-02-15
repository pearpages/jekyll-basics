# Basic Usage

> Changes to _config.yml are not included during automatic regeneration.

## Defining Source and Destination Folders in Config File

```yaml
source:      _source
destination: _deploy
```

Then the following two commands will be equivalent:

```
$ jekyll build
$ jekyll build --source _source --destination _deploy
```

## Don't forget to add YAML for processing

> Files in collections that do not have front matter are treated as static files and simply copied to their output location without processing.
