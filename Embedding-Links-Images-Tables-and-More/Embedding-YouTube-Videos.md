You can easily embed YouTube videos into your Markdown content. You Tube provides convenient embedding links that can be used to host YouTube videos directly in your own Html content with the ability to play inline and to jump to YouTube. 

Unfortunately embedded `<iframe>`'s don't work for all hosting platforms that may use your markdown, so Markdown Monster provides other ways to create and embed images links to YouTube as an alternative.

### YouTube Links
In order to embed a video you need a YouTube Url or Video Id:

* A YouTube Watch Url
* A YouTube Embed Url
* A YouTube ShortCut Url (`youtu.be`)
* A YouTube Video Id only

You can copy any of these YouTube URLs to your clipboard and the dialog will pick it up (if the Url is empty) or you can paste it in.

Markdown Monster can parse all of these using the @icon-youtube-play icon on the toolbar to embed a video:

![](https://github.com/RickStrahl/ImageDrop/raw/master/MarkdownMonster/EmbedYouTubeVideo.gif)

To do this:

* Pick up any YouTube Url or Video Id 
* Copy the Url or Id to the clipboard
* Position the cursor in your document
* Click on the **@icon-youtube-play Embed in YouTube** Toolbar button
* The Video Id is automatically picked up
* Alternately paste the Url or Id explicitly and MM fixes up the URL to get the Id.
* You see a preview
* Choose your Embedding Mode
* Click **Embed Video** to embed the video into the Markdown Document

> ##### @icon-warning IFrame Rendering requires that *Allow Script Tags in Markdown` is enabled
> Native YouTube embedding relies on `<iframe>` embedding which by default along with `<script>` tags is *disabled in MM*. To enable scripts and iframes you need to enable the **Allow Script Tags in Markdown** option on the menu or in Settings.
>
> You can enable the setting from the **Edit** menu or in **Settings**:
>
> ![](/images/AllowRenderScriptTags.png)

### YouTube Embedding Modes
Unfortunately YouTube videos or links into Markdown can be a little complicated **depending on your Markdown publishing platform** and what it supports for embedding external content. YouTube's native embedding tools for the live, interactive YouTube Video Player create `<iframe>` content that is not allowed by many platforms, specifically Github and other source code repositories.

To better support various platforms, Markdown Monster's YouTube embedding provides several different embedding modes.

#### Markdown Video Player Embedding 
Uses standard Markdown syntax to embed the YouTube Video Player into Markdown. The player is rendered into Html as an iframe and requires script code to run. It's embedded using default YouTube settings which uses fixed width rendering that doesn't resize larger and resizes awkwardly for smaller sizes.  
<small>*requires Allow Script Tags in Markdown Setting to be set and hosting platforms have to support iframe/scripts*</small>

```markdown
![Anti-Trust - War Machine](https://www.youtube.com/watch?v=3CM1_Ji6fJ8)
```

#### Html Video Player Embedding 
Uses raw Html to embed the YouTube Video player into the Markdown text. This offers more control over the player's layout and by default auto-sizes to the window width and properly resizes to smaller sizes.
<small>*requires Allow Script Tags in Markdown Setting to be set and hosting platforms have to support iframe/scripts*</small>


Embeds:
```html
<div style="position: relative; width: 100%; padding-bottom: 56.25%">
<iframe src="https://www.youtube.com/embed/3CM1_Ji6fJ8" 
        title="Anti-Trust - The War Machine" frameborder="0" allowfullscreen
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" 
        style="position: absolute; width: 100%; height: 100%;">
</iframe>
</div>
```

#### Image Link from Saved Cover Image
This option captures the YouTube cover page as shown in the previewer. The idea is to capture an image that **looks like the player** and then takes the user to YouTube to actually play the video. This works for platforms like Github that don't support iframe embedding. The image captured is saved to disk as a resource and has to be published to the hosting platform alongside the Markdown document.

```Markdown
[![Video: Anti-Trust-War Machine](Anti-Trust-WarMachine.jpg)](https://www.youtube.com/watch?v=3CM1_Ji6fJ8)
```

#### Embedded Cover Image Link Embedding  
Same as the previous option, but instead of saving the captured preview image to file, the image is embedded as image data content into the Markdown content in order to create a self-contained document. But note that this produces a large Markdown and HTML render file since the image content is essentially contained in the document.
Content is embedded as a link reference so the image data appears at the end of the Markdown file.

```markdown
[![Video: Anti-Trust - War Machine][1]](https://www.youtube.com/watch?v=3CM1_Ji6fJ8)

[1]: data:image/jpeg;base64,/9j/4AAQ...gJKiIgP/9k=
```

#### Linked YouTube Thumbnail (no play button)
This option embeds an image of one of YouTube's thumbnail images and adds a link that goes to the YouTube video when clicked. The thumbnail is a plain thumbnail without any YouTube branding or the play button. A text with the Video title is also created below the image to make it more obvious that you can navigate.


```markdown
[![Anti-Trust-War Machine](https://img.youtube.com/vi/3CM1_Ji6fJ8/maxresdefault.jpg)]  
 (https://www.youtube.com/watch?v=3CM1_Ji6fJ8)  

<small>*click image to [open video](https://www.youtube.com/watch?v=3CM1_Ji6fJ8)*</small>
```

### Capture YouTube Cover Image 
There's also a support feature available that lets you separately capture the content of the previewer as an image to the clipboard or to file.

![](/images/YouTubeCaptureTitleScreen.png)