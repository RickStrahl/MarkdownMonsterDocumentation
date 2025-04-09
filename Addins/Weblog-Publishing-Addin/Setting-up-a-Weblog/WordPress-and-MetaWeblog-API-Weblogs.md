WordPress and the MetaWeblog API are commonly used for publishing content via an API to a server. These formats commonly supported  by third party Weblog engines as it's a simple API that allows easy post management including posting, re-publishing and editing of posts.

### Configuring WordPress and MetaWeblog API
MetaWeblog and WordPress both use XmlRpc based interface that are fairly similar and roughly use the same mechanism to publish posts via an API. The API expects the post content as rendered HTML which is created as part of the publishing process. 

To work with this API you need to:

* Set the Blog Type to either `WordPress` or `MetaWeblogApi`
* Set the The API EndPoint URL
* Set the Username and Password

![](///images/CreateEditWebLogMetaWebLogWordPress.png)

* **Weblog API Url**  
This will be the MetaWeblog API or WordPress (v1) API endpoint that API requests are sent to. You need to know this URL or you can try to discover it.

  WordPress sites often use `xmlrpc.php` as the API endpoint like this: `https://yoursite.wordpress.com/xmlrpc.php` but the URL is not standardized for all sites that support it. You can check with your provider for the URL.
  
  Urls can be auto-discovered on the home page via a Meta-Data Tag if it exists. Click the @icon-gear button to try and auto-discover the API Endpoint.

  If you don't know the URL you can try using the @icon-gear  button to try and discover the API endpoint, which uses the site's home page and embedded meta tags that link to the RPC endpoint.

* **Preview Url (optional)**   
This is an optional field and can be used if the publishing process doesn't return a permalink to a new create or updated post. This is an override for when the url **is not returned** by the publishing API.

* **Username and Password**   
WordPress and MetaWeblog require a username and password to authenticate and you can provide those values in those two fields.

Once you're set up you can start creating new posts.


### Create new Weblog Post
A Weblog Post is just a Markdown document with related resources. When you create a new post we recommend you use the **Weblog -> New Weblog Post** menu to create it.

![](///images/NewWeblogPost.png)

Although recommended, **New Weblog Post** is not required. Any Markdown document can be published as a Blog post. But what **New Weblog Post** brings to the party is:

* Creates the post in a Weblogs folder that is organized by months
* Precreates a file name based on the title
* Adds the title as a header into the document

Now write your post using regular Markdown text. You don't have to worry about anything else in terms of how to format the document. The HTML you see in the preview is pretty much what will go to the server (for HTML based server APIs).

One thing you'll want to try and do is store images in the same folder or folder hierarchy as the Markdown file or use online URLs with images pointing at Azure Blob Storage or an Github  image dump. This will ensure that the post can find related resources reliably **and** that the preview can render the content properly. Don't worry about the final image locations - they will change and are fixed up when posts are published.

#### Publishing or Republishing a Post
When you're done writing your post content, you then need to publish the post. Click on the @icon-rss button in the toolbar or **Weblog -> Publish Weblog Post** from the menu to open the publish dialog:

![](///images/WeblogPublishingDialog.png)

Note that you don't have to manually create the meta data shown in the figure - it's generated as part of the **Publish Post** (or **Save MetaData**)  process.

The title is pre-filled from the title of your document (YAML `title` first if it exists, or the first `#` or `##` header) and you can fill in the rest of the fields. 

**Categories** and **Keywords** are comma delimited values.

#### `mt_markdown` implied Custom Field
When MM published a Wordpress or MetaWeblog API post it'll add an `mt_markdown` custom header explicitly to the post request which contains the raw markdown of this post including the meta data. This can be useful if the backend application has access to the post API and can pick up the raw Markdown to store along side the HTML for the post. 

This is useful to allow downloading of the same raw Markdown as part of post data to provide reliable two-way sharing of the Markdown data for post editing.

#### Send your own Custom Fields
The Markdown Monster post form also allows you to send your own **Custom Fields** that add to a post's meta data which can be useful if the server has access to this custom data.

The following example adds two custom fields for `mt_publishon` and `mt_location` which the server application uses to provide that info on a post. You can see these values in the screen shot above and it.

Here's what the post meta data from the form above looks like:

```yaml
---
title: Using Application Protocols to Open Desktop Applications from a Browser
abstract: Application Protocols allow you to open an application using either shell protocols using ShellExecute or a WebBrowser using syntax like `markdownmonster:open` or `markdownmonster:untitled`. This can be an easy and useful mechanism for launching applications especially from a browser.
categories: HTML, Web, .NET
keywords: Application Protocols, Execute, Binary, Launch
weblogName: Rick Strahl WordPress
postDate: 2020-05-16T08:53:08.0358185-10:00
customFields:
  mt_publishon:
    key: mt_publishon
    value: 05/10/2017 08:00
  mt_location:
    key: mt_location
    value: Maui, Hawaii
---
```

You can use **Save Metadata** to save the metadata into the Markdown document as a YAML header, or - more likely - you can just **Post to Weblog** which sends the post to the selected Weblog Configuration and which also saves the YAML header into the document. 

API publishing is very quick, but it depends on your API backend. My personal Website posts even most long posts in a second or two, while WordPress (free) can take upwards of 10 seconds. 

Done!

The publish process will add a few additional bits of information to the meta data - it'll pick up a `permalink` and post Id from the server after a new post was created so that you can later repost to the server with that same post id.

```YAML
postId: 1737405
permalink: https://weblog.west-wind.com/posts/2020/May/19/Using-WSL...
```

### Re-publishing a Weblog Post
Once you've published your post it's possible to re-publish from the post with changes and new resources etc. When you republish the post, MM uses the captured post id to republish the post and update the existing content and any of the image resources uploaded previously.

Simply make your changes in the original document you posted and then go through the same publish process we used above.