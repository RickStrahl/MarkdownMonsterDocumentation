The Weblog publishing pushes standard WordPress and MetaWeblog API requests to the server. However in addition to the standard data it also pushes the actual Markdown text to the server. This allows you to capture on the server, so you can later download it again for editing. 

### Posting
When posting to the server Markdown Monster passes:

* The `custom_fields` array
* Sets the `mt_markdown` entry

Note that this is not a standard, but Markdown Monster sends this value regardless of whether your server understands it or not - it'll just be ignored if the server doesn't know what to do with it. 

If you have a custom server implementation you can read the `mt_markdown` text on the server and save it as part of your post. This allows you to  render your HTML from the Markdown or perform further processing on the text. 

### Retrieving Posts
If you have a custom server and can control the MetaWebLog/Wordpress API implementation, you can also send the Markdown back to Markdown Monster by setting the `custom_fields` array and the `mt_markdown` value which allows for effect two-way editing of the content once downloaded from the server.

Markdown Monster will check for the `custom_fields::mt_markdown` field when retrieving posts from the server when using the **Download Blog Post** feature. If  present, the Markdown document from `mt_markdown` is used rather than the HTML in the body.

If this field is not present downloaded blog posts are parsed from HTML into Markdown which might not provide 100% accuracy due to the markdown conversion.





