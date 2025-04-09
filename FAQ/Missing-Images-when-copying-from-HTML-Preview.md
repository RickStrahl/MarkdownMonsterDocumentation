If you want to copy output generated in the preview **with local content** and paste that text into another application like Microsoft Word, you might find that images are not showing up in the paste target.

### Local Images are not reachable from Clipboard HTML
The problem here is that when you copy HTML to the clipboard, the HTML is copied **as is without any source location context**. If you have a local Markdown file with local images that are linked as **relative resources**, the paste operation on the target has no idea how to resolve the relative image URL because all it has is the raw HTML.

In other words: The target application has no idea where the images live and so can't embed them into the document.

> The missing local image behavior isn't a problem specific to Markdown Monster. You can open the preview document in a full browser (Shift-F12) and you'll find the exact same copy/paste behavior.

### Workaround: Use Explicit Image URLS
One work around is to use explicit image URLS in your markdown content that point at Web URLs. If you store images on a Web site (whether uploaded to an image store like Azure Blob Storage or via a published blog post on GitHub or other site) and link them using a full `https://` link then copy/paste works as expected.

If you are using local images you can also explicitly embed images with their full file paths which also allows a paste operation to resolve the image. But even that is unreliable because a Paste typically only **links** the image and doesn't embed so if the document moves to another machine it won't be there.

### Workaround: Embed Images Inline
You can also embed images directly into content, if you use the **Image Dialog** (alt-i).

![](/images/EmbedImageAsBase64.png)

This will embed the base64 text for the image as content into the document. This can significantly increase the size of the document and make the document hard to work with, but it's an option if you need to get 'portable' images into your document.

### Workaround: Print Document to Self-Contained HTML
Another option is that you can export the rendered output to a self-contained HTML document using **Save To -> Save To HTML -> Self Contained HTML File with Embedded Styles and Images**.

![](/images/SaveToHtmlSelfContained.png)

You can then open this document in your Web Browser of choice, copy the content, and paste it into Word or other application. Images and other related resources should be preserved.