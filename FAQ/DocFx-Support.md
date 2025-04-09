Markdown Monster supports a subset of DocFx functionality for previewing, so that the preview reflects some of the features available in DocFx documents.

* TIP, WARNING, NOTE, IMPORTANT box display support
* File and Code includes (`[!include]` and `[!code-csharp]`)
* Minimal `xref` support

There are two separate implementations:

* DocFx Render Extension (enabled in Settings)
* Official Microsoft DocFx Parser (enabled via Markdown Parser dropdown on status bar)

### The DocFx Markdown Render Extension
This implementation uses a Markdown Monster specific Render Extension that implements the supported DocFx features using a custom implementation of DocFx features. This is a more lightweight implementation that works directly with Markdown Monsters Markdown pipeline. This extension can happily co-exist with non-DocFx Markdown content with all MM features available.

To enable this feature:

* Go to **Tools->Settings**
* Type **DocFx** into the search box
* Check the **Parse DocFx** checkbox

### The Official Microsoft DocFx Markdown Parser
This implementation uses the official Microsoft DocFx Markdown Parser extensions for MarkDig (which is the same parser the MM uses) to render DocFx content. This implementation creates a custom Markdown Monster parser implementation that defers core rendering to the DocFx parser. 

To enable this feature:

* Go to Status Bar
* Find the the **Markdown Parser Dropdown** (MarkDig or DocFx)
* Set to **DocFx**

Although this is the official solution from Microsoft it's not directly geared towards rendering single documents as it's meant for generating entire sites of content, so not all features work in the context of previews. It also doesn't respect some of the Markdown Monster Markdown and document options so it should be used exclusively for DocFx content.

> When the **DocFx Markdown Parser** is enabled, it overrides the **Parse DocFx** Render Extension setting.

### Supported Features

#### Include Content Files
DocFx supports loading nested content from externally stored files using the following syntax:

```markdown
[!include[](includeFile.md)]
```

You can also specify files as relative paths:

```markdown
[!include[](../includeFile.md)]
```

or as 'site' relative paths (both work the same):

```markdown
[!include[](~/includeFile.md)]
[!include[](/includeFile.md)]
```

> #### @icon-info-circle Root Folder Resolution for `~/` and `/`
> Site Relative Paths are determined using the active documents `WebRootPreviewPath` which is set based on the document location and probing for specific files or settings in a project. Please see [this topic](VFPS://Topic/_5FZ0OZKLN) on how the root path is resolved for `~/` and `/`. For DocFx typically this is the `docfx.json` in the DocFx project's root folder.

#### Include Code Files
Likewise you can also inject code files with  specific syntax:

```markdown
[!code-csharp[](~/includeCode.cs)]
```

#### TIP, NOTE, WARNING, INFO, IMPORTANT
DocFx supports a number of special display boxes that let you highlight text and notes:

![](/images/DocFxHighlightBoxes.png)

You can use the following syntax:

```markdown
> [!WARNING]
> This is some Note Text  
> that spreads across two lines

> [!NOTE]
> Singe line note.

A block of text between note boxes.

> [!TIP]
> Tipping my hat to the clown

> [!IMPORTANT]
> Don't forget to screw on your hat!

```