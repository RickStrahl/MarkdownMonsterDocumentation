Markdown Monster's Preview Pane shows you what your markdown text looks like when rendered to HTML in close to real time while you are entering text. 

**The preview is updated whenever you briefly stop typing.**

The editor has a few special operations that affect the way the preview pane is handled:

* [Preview Toggling](#preview-toggling): On or off
* [Preview Location](#preview-location): Internal or External
* [Preview Sync](#preview-sync): How editor and preview sync
* [Preview Refresh](#preview-refresh): Frequency of Refresh
* [Preview Scroll Sync](#preview-scroll-sync)

### Preview Toggling
Markdown Monster's editor supports previewing of Markdown and HTML content as rendered HTML. The preview window can be toggled on and off in several ways:

* **F12** Shortcut Key
* Preview Toggle @icon-globe in the top Window menu next to the close box   
![](/images/PreviewWindowToggle.png)

* On the menu via **View -> Html Preview**


Any of these options will toggle the Preview Pane on and off if you are editing a Markdown, HTML or **untitled** (New) documents. 

Markdown Monster supports editing a variety of text file formats, but on HTML and Markdown documents present the Preview Pane - for all others toggling has no effect and there is no preview pane.

### Preview Locations
By default the preview Window is located **inline** of the main Markdown Monster window:

![](/images/ScreenShot.png)

Optionally you can also use an **external window** for the preview:

![](/images/externalpreview.png)

The external window can be **Docked to the main Markdown Monster Window** or can be free floating and optionally be set to float to the top of the Windows stack to always stay visible.

Using an external window can be useful to put the Preview output onto a separate screen.

![External Preview Window](https://github.com/RickStrahl/ImageDrop/raw/master/MarkdownMonster/ExternalPreviewWindow.gif)

To switch between modes use:

* **Views->Internal Preview** or **Views->External Preview Window**
* The dropdown next to the Globe icon in the Window Control toolbar


### Preview Refresh
In order to keep the editor responsive while typing the preview window is updated whenever you **stop typing for ~1/2 second**. This makes for optimal typing speed while still giving a reasonably real time text update for your HTML Preview.

For very large documents (1500+ lines) the no-typing timeout goes up to ~2 seconds.

### Preview Scroll Sync
In addition to showing changes as you type, the preview can also sync the editor and preview. 

Most commonly you want to scroll the editor and see the preview show the appropriate location as the editor is scrolled. Alternately you can also opt to have preview scrolling sync the editor and you can use both in combination. There are also options to not scroll the preview automatically and instead require manual sync via the `Ctrl` key or by clicking into the editor.

To this effect there are 5 Preview Sync Mode options:

* EditorToPreview *(default)*
* PreviewToEditor
* EditorAndPreview
* Navigation Only
* None

The setting can be configured in **File -> Tools -> Settings** with the `PreviewSyncMode` property or by using the rightmost statusbar icon dropdown:

![](/images/PreviewModeSelection.png)

> #### EditorAndPreview Sync Mismatches
> When you use preview mode **EditorAndPreview** you may find that occasionally the preview or editor won't line up properly. This can happen when working with large images or code blocks (or any other non-text objects) when the previewer can't find an appropriate element to sync to. 
>
> For most common scenarios this isn't a big problem, but if you run into frequently you might be better off to use  **EditorToPreview** sync mode rather than  on **EditorAndPreview**. You can still scroll the preview by scrolling the editor achieving a similar, but more consistent sync experience.

For best operation the default **EditorToPreview** sync mode works most reliably.

**EditorAndPreview** is useful if you frequently read your content in the previewer and browse around the document. Just remember that there may be occasional sync problems in this mode.

For best performance - especially in very large documents (100k words+) - turning syncing off and using **NavigationOnly** can improve typing performance. In this mode the previewer only refreshes when you click the mouse into the editor document, or you use the `Ctrl` key to force an explicit preview refresh in the previewer.

Finally **None** will not sync the editor and preview at all even using the force Preview.

### Forcing a Refresh of the Preview
If you one of the Editor Sync modes, you generally don't have to refresh manually, but there may be an occasional situation where the Preview doesn't automatically sync. In that case you can use:

* Press the `Ctrl` key to refresh and spellcheck
* Save the document using `Ctrl-s` or `Ctrl-shift-s`

Both operations force a full document refresh.

### Refresh Performance
For very large documents the preview refresh and spell checking can cause performance problems with the preview. Essentially the preview can take longer to refresh than the next auto-refresh interval which can cause annoying lag while typing as the editor is locked during the preview update.

For very large documents a recommendation is:

* Set Preview Sync to **Navigation Only**
* Manually refresh as needed with the `Ctrl` key