You can embed links into document content in several ways:

* Using the Link Dialog *(ctrl-k)*
* Using inline text linking  *(ctrl-shift-k)*
* Using raw Markdown Syntax
* Using raw HTML Syntax

### The Paste Link Dialog (ctrl-k)
You can use the **Link Dialog** by clicking on the @icon-external-link on the toolbar. The Paste Link dialog lets you interactively create a link to paste into your content. Here's what the dialog looks like:

![](/images/pastelinkdialog.png)

Although this is a UI dialog the flow through dialog can be very quick using shortcut keys:

* Select text then `ctrl-k` then `Enter` if clipboard hold link
* Select text `ctrl-k` then type link then `Enter`
* Select text `ctrl-k` then `Search Web` to open Browser, copy link, return then `Enter`

With the dialog up, if the Link field is empty and you have a URL on the clipboard, the link is automatically filled. This means if you have a URL on the clipboard when pressing `ctrl-k` the dialog is immediately filled, or if you open the dialog, then pick a URL in a browser or elsewhere, then return to Markdown Monster the URL is automatically filled in and you can simply press `Enter` to accept and embed the Markdown link.

For the Link you can either type in or paste a URL or use the file selection button pick a local file resource to link. Any local file resources will be linked as a relative path if possible.

> #### @icon-info-circle Automatic URL Embedding from Clipboard
> If you have a URL on the clipboard when the dialog is first opened, the URL is automatically placed into the **Link** field. This also applies to the Inline Link Shortcut operation below.

If you navigate off the form and copy a URL to your clipboard then return to the form, if the **Link** field is still empty it is then automatically filled from the Clipboard URL.

### Inline Link ShortCut (ctrl-shift-k)
If you don't like to use a UI form to pop up you can get similar behavior with `ctrl-shift-k` key combo which creates a link from the current selection of text and directly injects the markdown into the page. It fills the text part and if a URL is on the clipboard fills that into the link part. If not the cursor is placed into the link area for you to fill in the link. 

It's a quick way to get a link into the page from selected text.

### Using Raw Markdown
Of course you can also manually type the raw markdown text for a link. To embed links into a topic you can either use the markdown syntax like this:

```markdown
[Go to the Support Web Site](https://support.west-wind.com)
```

or for local links using relative paths:

```markdown
[Download Page](./product/download.html)
```

### HTML Syntax
Markdown also supports raw HTML so you can also use raw HTML text to embed links. This is useful if you require `target` links or need to add alignment styling.

```markdown
<a href="./product/download.html" target="_top">Download Page</a>
```

### Embed Web Links
There's also support for explicitly adding links from the Web based on a text selection in the editor. If the link you are embedding uses a searchable term - like a product name, or specific Web site for example - you can highlight the name and immediately jump to a link to embed, or open a browser search for that term.

There are two places and two mechanisms to use this quick link feature:

#### Mechanism

**Context Menu Web Search and Link**  

You can use this mechanism from the context menu on a text selection in the editor where the text selection becomes the search text to lookup:

![](/images/WebKeyWordSearchLink.png)


**Paste Link Dialog**

You can use the **Search and Link** button the **Paste Link Dialog** to do a quick search and select an item from the list: 

![](/images/WebKeyWordSearchDialog.png)


#### Operations
There are two different ways that a search and link operation can be performed:

* Directly search and Link (as shown above)
* Web Browser Search

The first is a context menu option where the selected text is used for a search and a list of the 10 first matches are returned from a Web search. The search returns the page title and link text and when you select the item the link is used to fill the Link in the dialog, or directly embeds the link into the Markdown link.

The **Web Browser Search** opens a Web Browser to a search page with the selected editor text as the search term pre-selected. You can then find a link to in the browser and copy it to your clipboard. When you return to Markdown Monster the link is picked up and either filled automatically into the Link dialog, or if you are directly embedding a link used for directly creating the Markdown link.