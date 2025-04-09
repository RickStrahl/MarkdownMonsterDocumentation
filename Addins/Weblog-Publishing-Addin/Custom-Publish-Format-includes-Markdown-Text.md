The Weblog publishing tools push standard WordPress and MetaWeblog API requests to the server. The default content format for posts in these formats use rendered HTML to send to the server. This works fine for rendering, but if you want to customize the render process and use the raw Markdown, or you want to pass the Markdown back and forth between server and client via Weblog Post downloads converting to and from HTML results in loss of document fidelity.

### Custom `mt_markdown` Field
However, Markdown Monster always pushes a customer `mt_markdown` field with every Weblog publish operation, and also looks for an `mt_publish` custom field on downloaded blog posts. This makes it possible to send Markdown to a server, and retrieve the original Markdown back in Markdown Monster when downloading a post. 

Keep in mind, `mt_markdown` is a non-standard field, which likely means that this is only useful in custom implementations that can access this field data as part of the WordPress or MetaWeblogApi interfaces.

### Sending Posts
When posting to the server Markdown Monster passes:

* The `custom_fields` array
* Sets the `mt_markdown` entry

Note that this is not a standard, but Markdown Monster always sends the `mt_markdown` value regardless of whether your server understands it or not - it'll just be ignored if the server doesn't know what to do with it.

### Retrieving Posts
Likewise Markdown Monster also checks for the `mt_markdown` custom field on incoming posts that are downloaded from a Weblog. If the custom  `mt_markdown` field exists, it is used to populate the post text placed in the editor, instead of converting the content from HTML to Markdown. 

This preserves the fidelity of the document and makes it possible to safely pass Markdown between client and server over multiple iterations.


> Note: If you store your posts locally and don't delete them another option for reliably updating server posts is to simply republish. Markdown Monster makes it very quick and easy to republish posts simply by resubmitting.