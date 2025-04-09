When rendering documents in the Preview for documents that eventually end up on a Web Site, you often end up with **site relative links** that use a site relative root path that starts with `/`.

For example if you have images with links like this on a Web site:

* `/images/test.png`
* `/.attachments/images/test.png` (VSTS)
* `~/images/test2.png`

the images are unlikely to render properly in the Preview, because MM **can't interpret the `/` or `~/` root path** without some help. It simply doesn't know what `/` or `~/` means in the context of only an open Markdown Document. By default, when MM renders topics it assumes the document's path as the **base path** for the document and so it really only works reliably when resolving **document relative** or **fully qualified paths**. But it **can't automatically resolve web root relative paths**, because it has no idea where the `/` path lives in your 'project'. 

Site Root Paths are important for a couple of reasons:

* **Preview Root Folder Location**  
This allows the Previewer to use the Site Root Path as the `basePath` in the rendered HTML document. All links are then rendered relative to this base path. This effectively mimics the behavior of a Web site root folder even if that location is not running as a Web site.

* **Relative Paths for Link and File Embedding**
This allows you to link or save files in a local folder location that can be resolved as a relative path to the Preview Root Path specified so that `/images` can resolve cleanly. It also ensures that `../` links are only followed up to the Root Path and don't embed crazy link `../../../` folder chains.

> #### @icon-warning Avoid Absolute File Paths
> Ideally you should **never** link a file using an absolute path as that only works on your local machine. Ideally everything should be linked as either a document relative path, or a 'site' relative path where `/` is a known root path location.

### Site Relative Path Overrides
To help with this Root Path problem, Markdown Monster allows you to specify a `previewWebRootPath` - a path that describes the **Project's Root Folder**. The idea is that you can now reference `/` as a path and resolve to this root path. Likewise links embedded can create a relative path that that can use `/` at its base as well as reliable link `../` up to the parent folder, but no further.


There are several settings that let you specify the Root Path <small>(*in order of processing priority*)</small>:

1. `previewWebRootPath` YAML header in the active document
2. `PreviewWebRootPath` in an open MM project <small>*(`.mdproj` file)*</small>
3. `.markdownmonster`, `_toc.json`, `docfx.json` file in a parent folder
4.  `<yourProject>.mdproj` project file in a parent folder

The easiest and most common approach is to just drop a marker file in **#3** in the project root folder. This is a one time configuration for an entire folder hierarchy.

#### YAML Header
The first and most localized way is by providing a YAML header in your Markdown document as:

```markdown
---
previewWebRootPath: c:\wikis\mywiki\
---

![](/test.png)
```

Once you add the header any link that references a path starting with `/` will use `c:\wikis\mywiki` as the base path for `\`. So `/images/screenshot.png` becomes `c:\wikis\mywiki\images\screenshot.png`.

To specify the YAML attribute you can add a YAML header to the document at the very top of the Markdown document:

You can use either full path as above or a document relative path:

```markdown
---
previewWebRootPath: ..\
---

![](/test.png)
```

If you want to be adventurous you can also use Web links:

```markdown
---
previewWebRootPath: https://markdowmonster.west-wind.com/
---

![](/test.png)
```

Which can work if you have all related resources that live images on a content Web site or CDN.

#### Project Setting
Markdown Monster has support for projects which is basically a collection of files or folders that you open and save as a collection in the editor. You can use **File -> Projects -> Save Project** to create a new project which captures the currently active documents that are open as well as the active folder.

The project also has a `PreviewWebRootPath` property that can be configured using the **Edit Project File** menu option:

```json
{
  "ActiveFolder": "C:\\projects\\MarkdownMonster\\samples",
  "ActiveSidebarIndex": 0,
  "OpenDocuments": [
    {
      "Filename": "C:\\projects\\MarkdownMonster\\SampleDocuments\\DocFx.md",
      "IsActive": true,
      "LastEditorLineNumber": 0,
      "LastImageFolder": null
    }
  ],
  
  // This sets the WebRootPath for all files rendered while the project is open
  "PreviewWebRootPath": "C:\\projects\\MarkdownMonster"
}
```

When this value is set it is applied to all documents when rendering links/images that start with a `/` - same as with the YAML header.

You can set this value to the default value of `null` if you don't want any overrides to occur on the project level.

If the `PreviewWebRootPath` property is not set the `.mdproj` file's path automatically is used.

#### `.markdownmonster` or `_toc.json` Files in Parent Hierarchy
You can also use a couple of special files in the 'root' folder that designates your Web root folder. If you have `.markdownmonster` or `_toc.json` files in a folder anywhere in the hierarchy of the current document that folder will be used as the preview Web root path.


####  Final Fallback: OS Root Directory
If none of the above apply the `/` resolution falls back to the OS path, which is likely never what you want, so I recommend you have one of the other solutions in place **or use document relative paths** instead.