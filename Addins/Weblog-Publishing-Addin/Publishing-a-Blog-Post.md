There are two ways you can publish a blog post: 

* Use an existing Markdown Document
* Create a new Weblog Post

In Markdown Monster a blog post is simply a markdown document with some associated **Metadata** attached at the top of the document, which is created when you are ready to publish your post. So in essence any document can serve as a new Weblog document.
    
However, there's also a **File -> New Weblog Post** option on the menu that creates a new folder, markdown document and adds default meta data to your document. 

> #### @icon-info-circle DropBox by Default
> By default Markdown Monster stores new blog posts in a folder on DropBox (if available) in a `Markdown Monster Blog Posts` folder. You can always pick a different location or override the `PostsFolder` setting in **Tools->Settings**, but these shared locations are great for accessing your blog posts from any machine connected to your Dropbox account.

When a Markdown document is published as a blog post, a bit of Meta data that contains the title, abstract, categories and keywords and optional custom fields can be added to the document. Most Weblog services can use this data to create the post online.

Here's the form you use to create a new Blog post, and publish your post:

![](//images/weblogaddinpublishpost.png)

When you click on **Post to Weblog** or **Save Metadata** a YAML block is added at the top of your markdown document as an HTML comment:

![](//images/weblogmetadata.png)

The post metadata includes all the info you entered in the dialog and is in  YAML format. When you later re-open the window to re-publish your entry this data is preloaded into the dialog and saved when you exit.

> **Note:** The meta data is stripped out before your post is published to the server. It is however sent with the raw Markdown in the mt_markdown custom fields.

When the post is published to the blog the meta data is parsed and injected into the API request to the server to tell it about the post to be posted using either **MetaWeblogApi** or the **Wordpress XML-RPC API**.

The Markdown is converted to HTML and posted as the Blog body. If all goes well your post should be published very quickly and when done a Web page should pop up displaying the post.

> #### @icon-info-circle Markdown Publishing to the Server
> Markdown Monster also adds the raw Markdown text when sending the blog posts in the MetaWebLog/Wordpress `custom_fields` data, setting an `mt_markdown` field within XML-RPC post data. This allows custom Web sites that listen for those fields to pick up and store the raw markdown, and more importantly also return this markdown when retrieving blog posts, making it easier for two-way editing.
>
> When reading posts from the server, Markdown Monster looks for the `custom_fields::mt_markdown` field and if it finds it in the request data loads its content into the Markdown editor. Otherwise the **body** is used and converted from Html.