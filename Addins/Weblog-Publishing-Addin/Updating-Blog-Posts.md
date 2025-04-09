Markdown Monster lets you easily publish blog posts and we recommend you store your blog posts in a central location in a folder. If you need to republish a post after initially publishing you can just re-open the original Markdown file, make your change and republish.

By default posts are created on your DropBox folder as `Markdown Monster Weblog Posts`. You can change the default path where posts are created in the settings configuration file.

To manage posts you typically have two options:

* Maintain posts locally (or DropBox)
* Download Posts from the server

Traditionally with tools like Live Writer you tend to publish posts and then later download them. This tends to work well with Live Write because it uses HTML for editing and simply redisplays the HTML that was posted.

However for Markdown Monster downloading just HTML - while it works using HTML to Markdown conversion - is not high fidelity as HTML has to be converted from HTML to Markdown.

There are a few options however.

### Storing Posts Locally
By default when you create a new post it's created in a new folder with the structure of the `Markdown Monster Weblog Posts\YYYY-mm\PostTitle`. Each post is dropped into its own folder so that you can also store associated images in this folder. 

![](//images/WebLogDropBoxFolder.png)

The idea is that you create self contained posts that include both the markdown text and the related images in an organized manner that you can later find again.

When you store posts locally you can always return to the post and open it  with Markdown Monster to edit the post and simply republish it. This is the best solution if available to you and the approach I use most of the time.

### Downloading Posts from the Server
If you have old posts that pre-date Markdown Monster, or you simply don't want to store your posts locally, Markdown Monster also supports downloading posts for editing. In this process posts are downloaded from the server and capturing the post text and images.

There are two ways this can work:

* HTML to Markdown Conversion
* Markdown from `mt_markdown` (server must support this)

#### Html to Markdown Conversion
If you are downloading you're probably working with the first choice - your post is simply stored as HTML on the server. 

In this scenario Markdown Monster downloads the post as HTML and then runs its Markdown to HTML conversion on the HTML. It will also download dependent images and store those in the same folder as the newly created Markdown document.

> #### @icon-warning HTML Imports are not Perfect
> It's not possible to maintain 100% compatibility with HTML to Markdown conversion, so don't expect documents to be perfect when downloaded via HTML import. In most cases you will have to adjust the resulting Markdown, or your Markdown might contain a fair amount of raw HTML (which is valid Markdown as well).

#### `mt_markdown` in Data
If the post includes Markdown (in `custom_fields` and the `mt_markdown` field) Markdown Monster will use the Markdown from the post as is an open it in the editor. 

> #### `mt_markdown` is a custom format
> This is a custom format that Markdown Monster uses piggy-backing on MetaWebLog's `custom_fields` extension. Unless you explicitly implement `mt_markdown` support on the server this is *not going to just work*.