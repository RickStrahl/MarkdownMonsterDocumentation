You can embed audio and video links into content using the Image markdown syntax using the Medial Links confiuration switch which is enabled by default. 

![](/images/MediaLinks.png)

## Enable Media Link Rendering
Media Linking is enabled by default, but it's controlled via a configuration setting in:

`Markdown.MediaLinks: true,`

or search for **Media Links** in the Settings Editor.

## Video Embedding
To embed video you can use the following syntax:

```markdown
**Absolute**

![Video](https://anti-trust.rocks/albums/TheArbiterOfTruth.mp4)

**Relative**

![Video](So%20What.mp4)
```

Styling for the embedded images is handled via the `video` tag in the `theme.css` file. By default the video image is embedded with `100%` width to fill the width of the document.

## Audio Embedding

```markdown
**Absolute**

![Audio](https://anti-trust.rocks/albums/SoWhat.mp3)

**Relative**

![Music](SpeculateSpeculate.mp3)
```

### You Tube Link Embedding

You can also embed YouTube links:

```markdown
![You Tube](https://www.youtube.com/watch?v=m9oUu1wHsDM)
```

> To get more control over YouTube embedding/linking use the dedicated [YouTube Embedding Dialog](VFPS://Topic/_69D0ZWCK0).