# wxr-generator

[![npm](https://img.shields.io/npm/v/wxr-generator.svg?style=flat-square)]()
[![](https://img.shields.io/github/issues-raw/firekylin/wxr-generator.svg?style=flat-square)]()
[![license](https://img.shields.io/github/license/firekylin/wxr-generator.svg?style=flat-square)]()

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

### new Importer(options)

Returns a new instance of Importer.

- options: 
   * name: site name
   * url: site url
   * description: site description
   * language: site language, default is en-US
   * base\_site\_url: same as url
   * base\_blog\_url: same as url

#### Example

```js
var Importer = require('wxr-generator');
var importer = new Importer({
  name: 'another wordpress blog',
  url: 'http://test.wordpress.com',
  description: 'this is another wordpress blog test',
  language: 'en-US'
});

// importer.addPost(...)
```
### addPost(options)

Adds new post for Importer object.

- options:
  * id: post Id, if not provied, random ID will be generated.
  * url: post permalink url.
  * slug: post slug name if it exists.
  * date: post create time.
  * title: post title.
  * author: post author, it equals author's login name.
  * content: post content
  * summary: post summary
  * comment_status: post comment status, default is `open`, it can be `open` or `closed`.
  * ping_status: post ping status, default is `open`, it can be `open` or `closed`.
  * password: post visit password if it should, default is empty.
  * categories: post categories, it's an array item. Every item should has `slug` and `name` prototype.
  * tags: post tags, it's an array item. Every item should has `slug` and `name` prototype.
  * image: id of attached image to use as featured image for this post

#### Example

```js
importer.addPost({
  id: 1,
  title: 'hello world',
  url: 'http://localhost/hello-world.html',
  slug: 'hello-world',
  date: '2017-07-03 10:00:00',
  author: 'admin',
  content: 'Welcome to WordPress. This is your first post. Edit or delete it, then start writing!',
  summary: 'Welcome',
  comment_status: 'open',
  ping_status: 'closed',
  password: '',
  categories: [{slug: 'life', name: 'Life'}, {slug: 'wp', name: 'wordpress'}],
  tags: [{slug: 'blog', name: 'Blog'}],
  image: 1000
})
```
### addPage(options)

Adds new page for Importer object. All parameters are same as `addPost(options)`.

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

### addAttachment(options)

Adds new attachment(image) for Importer object.

- options: 
   * id: attachment Id. If not provided, random ID will be generated.
   * url: attachment absolute url.
   * date: attachment create time.
   * file: attachment relative path if it exist.
   * title: attachment title.
   * author: attachment uploader.
   * description: attachment description.
   * post_id: post id relate to the attachment.
   * meta_data: other serialized attach meta data.

#### Exmaples

```js
importer.addAttachment({
  id: 5,
  url: "https://upload.wikimedia.org/wikipedia/commons/f/fc/Minka.jpg",
  date: "2015-10-05 00:27:25",
  file: "/wp-content/upload/2015/10/05/minka.jpg",
  title: "Fig. 1. Cats and puppies",
  author: "admin",
  description: "Fig. 1. Cats and puppies",
  post_id: 3
})
```

```
// Example of adding featured image with post
let i = 100 // i should exist as the index of a loop
const image = 'http://example.com/image.jpg'
const imageId = (image) ? randomNum() : '' // use a different number range from i to avoid overlaps

importer.addPost({
  id: i,
  title: 'title'
  slug: 'slug',
  date: '2020-01-01 00:00:00',
  author: 'admin',
  content: 'post content',
  summary: 'excerpt',
  comment_status: 'closed',
  ping_status: 'closed', 
  image: imageId
}) 

if(image){
  importer.addAttatchment({
    id: imageId,
    url: image,
    date: '2020-01-01 00:00:00',
    title: 'title',
    author: 'admin',
    post_id: i
 })
}
```
### addComment(options)

TODO

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
