---
title: SNworks Developer Docs - DocSync

toc_footers:
  - <a href="http://getsnworks.com">Main Site</a>
  - <a href="http://thesnews.github.io/slate-guides/">Guides Dev Docs</a>
  - <a href='http://confluence.getsnworks.com/display/ID/Internal+Documentation+Home'>SNworks Internal Docs</a>
  - <a href="http://confluence.getsnworks.com">Client Support Docs</a>
  - <a href="http://uptime.getsnworks.com/">System Status</a>
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

search: true
---

# DocSync Plugin

The DocSync plugin provides access to synced Issuu and ScribD documents. It provides a ton more functionality over the previous Issuu and ScribD plugins

> Load the helper and grab and the most recent Issuu document

```html
{% helper docSyncDocument %}
{% set doc = docSyncDocument.issuu.order('created', 'desc').first() %}
<a href="{{doc.url}}"><img src="{{doc.urlPreview}}" />
```

Using the updated fluent syntax you can easily grab and filter documents for both Issuu and Scribd.

Using the fluent interface you can easily limit, sort, search in folders and tags:

 * `order('WHAT ORDER')` - Order the results, usually this is just 'created desc' for the most recent
 * `limit(NUMBER)` - Limit number of returned results
 * `inFolder('FOLDER NAME')` - Fetch documents that are part of a collection (ScribD) or stack (Issuu)
 * `withTags('TAG1', 'TAG2', ...)` - Fetch documents with given tags (ScribD only)
 * `find()` - Fetch the items based on the filters
 * `first()` - Fetch and return only the first item that matches the filters

# Meta Properties

Each document system (Issuu and ScribD) provides a number of different meta properties. The plugin tracks everything that comes with the sync under the `meta` property. For instance - you can use `{{doc.meta.title}}` to get the file title for ScribD docs, or `{{doc.meta.name}}` in Issuu.

### Issuu Meta Properties

 * meta.username
 * meta.name - file name
 * meta.documentId
 * meta.uploadTimestamp
 * meta.created
 * meta.title - file title
 * meta.access
 * meta.orgDocType - original document type (i.e. pdf)
 * meta.orgDocName - original file name
 * meta.likes
 * meta.commentsAllowed
 * meta.pageCount
 * meta.publicationCreationTime
 * meta.publishDate
 * meta.publicOnIssuuTime
 * meta.description
 * meta.folders - array of folder ids
 * meta.coverWidth
 * meta.coverHeight
 * meta.embed - **embed is only available with pro accounts**

### ScribD Meta Properties

 * meta.doc_id
 * meta.title
 * meta.description
 * meta.thumbnail_url
 * meta.conversion_status
 * meta.page_count
 * meta.when_uploaded
 * meta.when_updated
 * meta.block_count
 * meta.reads
 * meta.authors


### Common Helpers

In addition to the meta properties, the plugin also provides simple accessors to common properties

 * `url` - url to the original document
 * `urlPreview` - url for the document thumbnail

```html
{% helper docSyncDocument %}
{% set doc = docSyncDocument.issuu.inFolder('My Sweet Folder').first() %}

<a href="{{doc.url}}">
    <img src="{{doc.urlPreview}}" />
    View {{doc.meta.title}}
</a>
```

# Examples

## Example: Issuu document in a stack

```html
{% helper docSyncDocument %}
{% set doc = docSyncDocument.issuu.inFolder('My Sweet Folder').first() %}
<a href="{{doc.url}}"><img src="{{doc.urlPreview}}" />
```

Using the `inFolder` method you can select only those docs that are part of a collection (ScribD) or stack (Issuu).

## Example: ScribD documents in a folder with a tag

```html
{% helper docSyncDocument %}
{% set docs = docSyncDocument.scribd
    .inFolder('My Sweet Folder')
    .withTags('tagname1')
    .find() %}

{% for doc in docs %}
    <a href="{{doc.url}}"><img src="{{doc.urlPreview}}" />
{% endfor %}
```

Using the `inFolder` and `withTags` methods you can filter by collection and tag.

