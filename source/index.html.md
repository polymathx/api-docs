---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
#   - shell
#   - ruby
#   - python
  - json

toc_footers:
  - <a href='https://polymathx.com/#contact'>Sign Up for a Polymath CMS Account</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Polymath CMS API! You can use our API to access Polymath API endpoints, which can get information on various contents, images, assets, data models, and leads in our database.

You can view API response examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right. PHP examples will be added soon.

# Authentication

> Example response from a base authentication

```json
{
  "_view": "API_INDEX",
  "_views": 1,
  "user": {
  "id": 1,
  "name": "Test Response",
  "owner": 1,
  "added_by": "system",
  "logo": "data:image/png;base64",
  "created_at": "2017-02-08T06:20:31.161Z",
  "updated_at": "2017-02-03T01:11:07.185Z",
  "url": "http://yoururl.com",
  "api_key": "yourapikey"
},
  "sources": { 
    "content": "https://api.polymathx.com/contents",
    "contacts": "https://api.polymathx.com/contacts",
    "media": "https://api.polymathx.com/media" 
  }
}
```

> Make sure to authenticate with your API key.

Polymath uses API keys to allow access to the API. Your company account owner can give you access to retrieve, and reset this key in the [content management portal](https://app.polymathx.com).

The API expects for the API key to be included in all API requests to the server in a GET or POST that looks like the following:

`https://api.polymathx.com/?key=yourapikey`

Required Global Parameter | Description
---------- | -------
key | The API key, found in the "Company" section of your CMS portal.

<aside class="notice">
You must replace <code>yourapikey</code> with your personal API key, and add this parameter on ALL API requests.
</aside>

# Contents

CMS contents are the primary data set from the CMS. All your website content can be accessed through the content endpoints, including SEO contents associated with each content set. 

## Get Content by Slug

Retrieve a single piece of content by its slug. 

> https://api.polymathx.com/contents/:slug

```json
{
  "id": 20,
  "model_type": 3,
  "name": "Example Content",
  "slug": "example-content",
  "content": { /* Data object here, based on content model */},
  "created_at": "2017-01-09T00:45:36.561Z",
  "updated_at": "2017-01-09T00:45:36.561Z",
  "draft": null,
  "primary_image": null,
  "secondary_image": null,
  "attachment": null,
  "seo": {
    "title_tag": null,
    "meta_description": null,
    "meta_robots": null,
    "canonical": null,
    "remove_from_sitemap": null
  }
}
```

### HTTP Request

`GET https://api.polymathx.com/contents/<SLUG>`

### URL Parameters

Parameter | Description
--------- | -----------
SLUG | The slug of the content you need to retrieve

<aside class="notice">
Make sure none of your content shares slugs across different models. Support for specifying a model will be added soon.
</aside>

## Get Content Models

Get an array of all of your content models.

> https://api.polymathx.com/contents

```json
[
  {
    "id": 1,
    "name": "Blog Post",
    "sitemap": null,
    "contents": "https://api.polymathx.com/contents/model/1"
  },
  {...},
  {...}
]
```

### HTTP Request

`GET https://api.polymathx.com/contents`


## Get all Content from Model

Get an array of all content items within a model.

> https://api.polymathx.com/contents/model/:model_id

```json
[
  {
    "id": 9,
    "name": "contact",
    "slug": "contact",
    "content": {/* Data object here, based on content model */},
    "primary_image": null,
    "secondary_image": null,
    "attachment": null
  },
  {...},
  {...}
]
```

### HTTP Request

`GET https://api.polymathx.com/contents/model/<MODEL_ID>`

### URL Parameters

Parameter | Description
--------- | -----------
MODEL_ID | The ID of the model that you want to retrieve contents from.


# Media

Media are distributed over the API in the form of CDN-hosted image URLs, and metadata. Images can be fetched from their ID, or in groups from their parent media group. 

## Get Media from ID

> https://api.polymathx.com/media/:media_id

```json
{
  "id": 22,
  "name": "something.jpg",
  "description": null,
  "alt_text": null,
  "created_at": "2017-11-30T21:07:28.477Z",
  "updated_at": "2017-11-30T21:07:28.477Z",
  "file": {
    "name": "something.jpg",
    "urls": {
      "hero": "https://cdn.polymathx.com/media/321/hero/something.jpg",
      "thumb": "https://cdn.polymathx.com/media/321/thumb/something.jpg",
      "medium": "https://cdn.polymathx.com/media/321/medium/something.jpg",
      "original": "https://cdn.polymathx.com/media/321/original/something.jpg"
    }
  }
}
```

Get the image content, and meta data from an image ID.

### HTTP Request

`GET https://api.polymathx.com/media/<MEDIA_ID>`

Parameter | Description
--------- | -----------
MEDIA_ID | The ID of the media item you are attempting to retrieve.

<aside class="notice">
Image sizes come in <code>hero</code>, <code>thumb</code>, <code>medium</code> and <code>original</code> by default. Cycle through these accordingly for better site speed, and quicker development.
</aside>

## Get Media Groups

Returns an array of all media groups.

> https://api.polymathx.com/media

```json
[
  {
    "id": 342,
    "name": "Homepage Carousel",
    "description": "This group contains images for the homepage carousel."
  },
  {...},
  {...}
]
```

### HTTP Request

`GET https://api.polymathx.com/media`

## Get all Media from Media Group

Returns an array of images from the media group specified.

> https://api.polymathx.com/media/groups/:group_id

```json
[
  {
    "id": 22,
    "name": "something.jpg",
    "description": null,
    "alt_text": null,
    "created_at": "2017-11-30T21:07:28.477Z",
    "updated_at": "2017-11-30T21:07:28.477Z",
    "file": {
      "name": "something.jpg",
      "urls": {
        "hero": "https://cdn.polymathx.com/media/321/hero/something.jpg",
        "thumb": "https://cdn.polymathx.com/media/321/thumb/something.jpg",
        "medium": "https://cdn.polymathx.com/media/321/medium/something.jpg",
        "original": "https://cdn.polymathx.com/media/321/original/something.jpg"
      }
    }
  },
  {...},
  {...}
]
```

### HTTP Request

`GET https://api.polymathx.com/media/groups/<GROUP_ID>`

Parameter | Description
--------- | -----------
GROUP_ID | The ID of the media group you are attempting to retrieve.

# Contacts

> https://api.polymathx.com/contacts

```json
[
  {
  "id": 1812,
  "contact_type": "contact",
  "content": {
    "name": "Timmy Chimichanga",
    "email": "timbo@gmail.com",
    "message": "I want to inquire about chimichangas."
  },
  "tag": "fresh"
  },
  {...},
  {...}
]
```

Returns an array of leads/contacts.

Contacts are the leads you have collected through your website's contact forms.  Contacts are returned as an array of all your contacts. Ability to filter by `form_id` coming soon. 

### HTTP Request

`GET https://api.polymathx.com/contacts`

# Website SEO

> https://api.polymathx.com/meta

```json
{
  "title_suffix": "Your Site Name",
  "robots": "##robots.txt contents",
  "meta_robots": "index, follow",
  "webmaster_verification": "<!-- Some string of HTML with your verification scripts in it -->",
  "header_analytics": "<script>//some header script string</script>"
}
```

Website SEO is returned as a JSON blob of all global meta data associated with your website.

This content is intended to be used on every page of your website, in the meta section. It also includes the contents of the robots.txt file for your website.

### HTTP Request

`GET https://api.polymathx.com/meta`

# Sitemap Data

> https://api.polymathx.com/sitemap

```json
{
  "maps": [1,2],
  "contents": {
    "1": [
      {
        "slug": "example-slug",
        "updated_at": "2017-04-22T22:03:35.765Z",
        "model_type": 1
      },
    ],
    "2": [
      {
        "slug": "example-slug2",
        "updated_at": "2017-04-22T22:03:35.765Z",
        "model_type": 2
      },
    ]
  }
}
```

Sitemap data is returned as a JSON blob that includes all information needed to build a sitemap for all your website content.

### HTTP Request

`GET https://api.polymathx.com/sitemap`



<!-- # Kittens -->

<!-- ## Get All Kittens



This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete -->

