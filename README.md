# Models

WordPress plugin to create custom post types and taxonomies using JSON, PHP or YAML files.

## Installation

**Please note:**  If you are updating to v1.0.3, the new default folder has changed from `model-json/` to `model-config/`

#### Composer:

Recommended method; [Roots Bedrock](https://roots.io/bedrock/) and [WP-CLI](http://wp-cli.org/)
```shell
$ composer require soberwp/models
$ wp plugin activate models
```

#### Manual:

* Download the [zip file](https://github.com/soberwp/models/archive/master.zip)
* Unzip to your sites plugin folder
* Activate via WordPress

#### Requirements:

* [PHP](http://php.net/manual/en/install.php) >= 5.6.x

## Setup

By default, create folder `model-config/` within the active theme directory. 

Alternatively, you can define a custom path using the filter below within your themes `functions.php` file; 
```php

add_filter('sober/models/path', function () {
    return get_stylesheet_directory() . '/your-custom-folder';
});
```

That's it, now go ahead and add `model-name.json` files, (`.php` and `.yaml` formats supported from v1.0.3) in the folder or subfolders to begin creating your models. Use [Unravel](https://github.com/soberwp/unravel) to move the config files outside of your theme path. 

## Usage

The data structure follows a similar data structure to WordPress taxonomies and post types arrays, so if an config option is missing from the examples below, follow the developers reference and place within `"config": {}`

If values are not specified, defaults are the same as WordPress defaults. 

Extracted examples presented below are in JSON format.

### Post Types

Create a custom post type. 

#### Required:

* [post-type-required.json](.github/json/post-type-required.json)
* [post-type-required.php](.github/php/post-type-required.php)
* [post-type-required.yaml](.github/yaml/post-type-required.yaml)

```json
{
  "type": "post-type",
  "name": "book"
}
```

#### Basic:

* [post-type-basic.json](.github/json/post-type-basic.json)
* [post-type-basic.php](.github/php/post-type-basic.php)
* [post-type-basic.yaml](.github/yaml/post-type-basic.yaml)

```json
{
  "type": "cpt",
  "name": "book",
  "supports": [
    "title", "editor", "thumbnail"
  ],
  "labels": {
    "has_one": "Book",
    "has_many": "Books",
    "text_domain": "sage"
  }
}
```

In the above example, `"labels": {}` are redundant because `"Book"` and `"Books"` would have been generated from `"name"`.

#### Multiple:

* [post-type-multiple.json](.github/json/post-type-multiple.json)
* [post-type-multiple.php](.github/php/post-type-multiple.php)
* [post-type-multiple.yaml](.github/yaml/post-type-multiple.yaml)

```json
[
  {
    "type": "cpt",
    "name": "book",
    "supports": [
      "title", "editor", "thumbnail"
    ]
  },
  {
    "type": "cpt",
    "name": "album",
    "supports": [
      "title", "editor", "comments"
    ]
  }
]
```

#### All Fields:

* [post-type-all.json](.github/json/post-type-all.json)
* [post-type-all.php](.github/php/post-type-all.php)
* [post-type-all.yaml](.github/yaml/post-type-all.yaml)

#### Post Type Tips:

* `"active": false` stops the post type from being created. Default is set to `true`.
* `"type": "post-type"` also accepts a shorthand `"type": "cpt"`;

### Taxonomies

Create a custom taxonomy.

#### Required:

* [taxonomy-required.json](.github/json/taxonomy-required.json)
* [taxonomy-required.php](.github/php/taxonomy-required.php)
* [taxonomy-required.yaml](.github/yaml/taxonomy-required.yaml)

```json
{
  "type": "taxonomy",
  "name": "genre"
}
```

#### Basic:

* [taxonomy-basic.json](.github/json/taxonomy-basic.json)
* [taxonomy-basic.php](.github/php/taxonomy-basic.php)
* [taxonomy-basic.yaml](.github/yaml/taxonomy-basic.yaml)

```json
{
  "type": "tax",
  "name": "genre",
  "links": [
    "post", "book"
  ],
  "labels": {
    "has_one": "Book Genre",
    "has_many": "Book Genres",
    "text_domain": "sage"
  }
}
```

`"links": (string|array)` assigns the taxonomy to post types. Defaults to `"links": "post"`

#### Multiple:

* [taxonomy-multiple.json](.github/json/taxonomy-multiple.json)
* [taxonomy-multiple.php](.github/php/taxonomy-multiple.php)
* [taxonomy-multiple.yaml](.github/yaml/taxonomy-multiple.yaml)

```json
[
  {
    "type": "category",
    "name": "genre",
    "links": "book"
  },
  {
    "type": "tag",
    "name": "author",
    "links": "book"
  }
]
```

`"type": "category"` and `"type": "tag"` shorthands are explained below under Tips.

#### All Fields:

* [taxonomy-all.json](.github/json/taxonomy-all.json)
* [taxonomy-all.php](.github/php/taxonomy-all.php)
* [taxonomy-all.yaml](.github/yaml/taxonomy-all.yaml)

#### Taxonomy Tips:

* `"active": false` stops the taxonomy from being created. Default is set to `true`.
* `"type": "taxonomy"` also accepts shorthands;
  * `"type": "tax"`
  * `"type": "category"` or `"type": "cat"` creates a category taxonomy.
  * `"type": "tag"` creates a tag taxonomy.

## Updates

#### Composer:

* Change the composer.json version to ^1.0.3**
* Check [CHANGELOG.md](CHANGELOG.md) for any breaking changes before updating.

```shell
$ composer update
```

#### WordPress:

Includes support for [github-updater](https://github.com/afragen/github-updater) to keep track on updates through the WordPress backend.
* Download [github-updater](https://github.com/afragen/github-updater)
* Clone [github-updater](https://github.com/afragen/github-updater) to your sites plugins/ folder
* Activate via WordPress

## Social

* Twitter [@withjacoby](https://twitter.com/withjacoby)
