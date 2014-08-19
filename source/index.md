---
title: SNworks Developer Docs

toc_footers:
  - <a href="http://getsnworks.com">Main Site</a>
  - <a href="http://thesnews.github.io/slate-guides/">Guides Dev Docs</a>
  - <a href='http://confluence.getsnworks.com/display/ID/Internal+Documentation+Home'>SNworks Internal Docs</a>
  - <a href="http://confluence.getsnworks.com">Client Support Docs</a>
  - <a href="http://uptime.getsnworks.com/">System Status</a>
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

```html
# Code will show up over here.
<a href="#">foo</a>
```

SNworks Developer Docs for Gryphon Sites. If you're looking for Guides, <a href="http://thesnews.github.io/slate-guides/">look here</a>.

#  Technologies we use

This information is on our <a href="http://confluence.getsnworks.com/display/ID/Documentation+Index">private help section</a>.

# Whaddya say?

<aside class="notice">
Learn the SNworks Lingo
</aside>

* **Apache** - Web server software
* **AWS** - Amazon Web Services. This is the cloud architecture we run our services on.
* **Bucket** - A top-level "folder" on S3.
* **CDN** - Content Delivery Network. A series of servers around the globe that server static assets (like CSS files and site images)
* **CloudFront** - The AWS CDN
* **DNS** - Domain Name System. Essentially the internet phonebook. Matches IP addresses to human-readable domain names (e.g. statenews.com)
* **EC2**  - Elastic Compute Cloud. Virtual servers
* **Git** - The source control management tool we use to manage code changes
* **HAProxy** - Software load balancer
* **LESS** - LESS is a superset of CSS that allows for mixins and proper namespacing. It compiles down to plain old CSS.
* **Load Balancer** - A server that redirects requests to multiple backend servers
* **Production** - The live server cluster. Only a privileged few ever see the internals here.
* **RDS** - Relational Database Service. Virtual database servers
* **Route53** - AWS DNS service
* **RTP** - Release(d) To Production. Code change has been queued for automatic deployment to production.
* **S3** - Simple Storage Service. The place we store media files and static site assets.
* **Stage** - The server cluster on which we test out new features and changes
* **Unable to Repro** - Unable to reproduce the error/issue/bug/feature in the request. We cannot fix what we cannot reproduce.
* **Varnish** - Cache server software
* **WOC** - Waiting on client
* **Won't Fix** - Error/issue/bug/feature is not an error, how the system normally functions and won't be addressed.

# Bitbucket and Git
## Overview

```shell
# Code sample here
```

```html
<a href="#">foo</a>
```

## Helpful Commands

```shell
user> git checkout
```
checkout something

# Dev Web Server

More information on this in our <a href="#">private help docs</a>.

# Twig Extensions and Tips

Overview

## Fetch Tag

## Helper Tag

> Load the config helper, and grab a value

```html
{% helper config %}
{{ config.get('foo.bar') }}
```

> Load the config helper, but call it 'Configuration'

```html
{% helper config as Configuration %}
{{ Configuration.get('foo.bar') }}
```

The helper tag loads Gryphon specific Twig helpers.

Parameter | Description
--------- | -----------
as STRING | Provide an alternate name for the helper (OPTIONAL)

## Config Helper

```html
{% helper config %}

Welcome to <a href="{{config.get('publication.url)}}">{{config.get('publication.name')}}</a>
```

The config helper provides read access to the global configuration system. **This helper has only one method: `get`.**

Common, but not all, config options used in templates:

Config key | Description
---------- | -----------
publication.name | Yeah...
publication.url | The canonical URL for the publication
mail.admin | The default admin email address
gryphon.media.meta | An array of meta properties
gryphon.default.section | The section that constructs the front page
gryphon.comments.disqus_shortname | The site's Disqus shortname

## Request Helper

# Coding for Gryphon

Creating templates for Gryphon is fairly simple once you have the basics down.

## base.tpl

## article/main.tpl

## article/templates

## author/main.tpl

## blog/

## gallery/

## main/

## multimedia/

## page/

## search/

## section/

## view/

# Macros

## article

## disqus

## render

## tools

# Gryphon CMS

# Using Third-party Services

## Working with Issuu

<!-- # Authentication

> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import 'kittn'

api = Kittn.authorize('meowmeowmeow')
```

```code
# With code, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace `meowmeowmeow` with your personal API key.
</aside>

# Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import 'kittn'

api = Kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```code
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Isis",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/kittens`

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
import 'kittn'

api = Kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```code
curl "http://example.com/api/kittens/3"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Isis",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">If you're not using an administrator API key, note that some kittens will return 403 Forbidden if they are hidden for admins only.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the cat to retrieve -->

