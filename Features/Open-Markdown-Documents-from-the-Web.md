Markdown Monster supports opening Markdown documents directly from the Web by providing a URL to a Markdown document. You can use **File -> Open From... -> Open from URL** which brings up a URL dialog like this:

![](/images/openfromurl.png)

MM then downloads and opens that document in the editor, optionally fixing up related image content.

The URL specified should point either to a raw Markdown Url that returns Markdown text, or can point at a few well-known sites using high level URLs rather than the raw document Urls.

The Url can fix up the following types of links:

* GitHub Markdown Documents 
* BitBucket Markdown Documents
* GitHub Markdown Gists
* Microsoft Docs Links

For any of these you can point at the top level display links and MM tries to figure out the raw Markdown URL for you.

### Fix up Image Links
If you simply grab a Markdown document and that document contains images that have relative image links, these images display as broken images because the images are not available locally.

Fix up image links expands image links to fully qualified image URLs and replaces the relative links in the page so that images can display properly.