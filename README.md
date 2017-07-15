# wxr-generator

XML(WXR) file generator for fully support official [WordPress Import Plugin](https://wordpress.org/plugins/wordpress-importer/). Inspired By [node-wxr](https://github.com/f1nnix/node-wxr).

## Install

```shell
npm install wxr-generator
```

## How To Use


```js
var Importer = require('wxr-generator');
var importer = new Importer();

importer.addCategory({
  slug : "perfect-category",
  name: "Perfect Category"
});

console.log(importer.stringify());
```

## API

### new Importer()

Returns a new instance of Importer.

#### Example

```js
var Importer = require('wxr-generator');
var importer = new Importer();

// importer.addPost(...)
```

### addCategory(options)

Adds new category for Importer object.

- options:
   * id: category Id. If not provided, random ID will be generated.
   * slug: category slug. Used in URLS, e.g. "js-rocks"
   * name: category title, e.g. "Everything about JS"
   * parent_id: category parent id if it existed.
   * description: category description string, default is empty.

#### Example

```js
importer.addCategory({
  id: 5,
  parent_id: 3,
  name: "Everything about JS",
  slug: "js-rocks",
  description: "tech about js"
})
```

### addTag(options)

Adds new tag for Importer object.

- options:
   * id: tag Id, if not provied, random ID will be generated.
   * slug: tag slug. Used in URLS, e.g. "js-rocks"
   * name: tag title, e.g. "JS"
   * description: tag description string, default is empty.


#### Example

```js
importer.addTag({
  id: 5,
  name: "JS",
  slug: "js-rocks",
  description: "tech about js"
})
```

### addUser(options)

Add new user for Importer object.

- options: 
   * id: user Id
   * username: user login name
   * email: user email
   * display_name: user nickname
   * first_name: user first name
   * last_name: user last name

### stringify()

Generates result XML (WXR) string for importing to Wordpress.

#### Example

```js
var importer = new Importer();

// importer.addPost(...)

var xmlString = importer.stringify();
require("fs").writeFile("export.xml", xmlString, function(err) {
  if (err) {
    console.log(err);
  }

  console.log("File was saved! Now it's time to import.")
});
```
## Contributing

Contributions welcome!

## License

[MIT](https://github.com/firekylin/wxr-generator/blob/master/LICENSE)