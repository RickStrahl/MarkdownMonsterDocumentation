#### ApplicationTheme
The application theme determines the application major theme for the window and controls. 

* Dark
* Light

>  @icon-exclamation-circle Any changes made to the ApplicationTheme requires a restart of Markdown Monster to properly render all the theme changes.

#### EditorTheme 
The theme used by the Markdown editor. A variety of themes can be used including `twilight`,`visualstudio`,`github`,`monokai`, `mono_industrial`.  You can also change the editor theme via the drop down on the bottom right of the form. These themes are stored in the `Editor\scripts` folder with a `theme-`.

#### PreviewTheme  
The theme used by the HTML Preview browser. Several themes are available including `Dharkan`, `Blackout`, `GitHub`, `Hipster`. You can also change the preview theme via the drop down on the bottom right of the form. These themes are fairly simple plain HTML themes and can be easily created or modified to match whatever style you want to see in the previewer. Look in the `PreviewThemes` folder.

#### PreviewSyncMode
Determines if and how the Preview window is synced with the editor. The following values can be used:

* EditorToPreview
* PreviewToEditor
* EditorAndPreview
* None

#### UseSingleWindow
If `true` opens all documents in a single window. This is the default and preferred mode to operation Markdown Monster, but you can also force MM to open every opened externally in a new instance of Markdown Monster. 

> Note if running without SingleWindow mode you may see inconsistent behavior in the **Recent Documents** list if multiple instances are open.

#### OpenInPresentationMode
If set to `true` starts the editor in presentation mode that displays the rendered HTML in full screen mode.

#### PreviewHttpLinksExternal
If set the `true` all preview links that are `http://` or `https://` links are opened externally in your default system Web browser. If `false` links open in the previewer. We recommend you leave the default of `true`.

#### ShowFullDocumentPathInTitleBar
If `true` displays the full path to the open file. Default is `false`.

#### DistractionFreeModeHideOptions
This flag lets you configure what UI components are hidden in distraction free mode as well as a couple of mode settings (**maximized** and **maxwidth:width**). Distraction free mode is accessed via the @icon-arrows-alt icon on the Window bar or via **Alt-Shift-Enter**.

This option takes a comma delimited list of the following values you can hide:

```text
"toolbar,statusbar,menu,preview,tabs,maximized,maxwidth:970"
```

Each of the items included is **hidden** (except for maximized and maxwidth obviously). Any of these values included hide the corresponding UI item. Any option can be left out to not hide that item. 

**maximized** when provided maximizes the window, **maxwidth:970** allows you to specify a maxwidth for the editor's content area which allows you to optionally provide lots of whitespace around text as is common in distraction free modes. The number is the width in pixels.


#### AutoSaveDocuments
If `true` automatically saves documents to disk as you type. Document and file are always nearly in sync (except for the 1 second or so no-typing delay before text is updated). This setting overrides the **AutoSaveBackups** option if set. No backups are created if this option is `true`.

#### AutoSaveBackups
Set this option to `true` to backup your working files while you are working, but before they are saved. In case of a crash the backup document is opened in addition to the actual document so you can compare or choose the recovered content. No backups are created if **AutoSaveDocuments** is `true`.

#### AlwaysUsePreviewRefresh
Determines whether the Preview is always refreshed fully or (default) just replacing the existing content. The default behavior of content replacement is quicker with less flicker, but cannot update embedded scripts or other dynamic content.

If you are embedding dynamic content that includes script tags or expanding widgets set this flag to `true`.



#### ImageEditor
Lets you specify an image editor to edit images. Used for right clicking on images in your Markdown text, or via the Folder Browser. Defaults to **Paint.NET** if installed, otherwise falls back to **Paint** as the default.

#### ImageViewer
Optionally lets you specify an external image viewer. Defaults to `null` which uses the system viewer (Photos typically). Note that MM automatically previews images in the editor as you click on them so this is not required often.

#### WebBrowserPreviewExecutable
This allows you to explicitly specify a Web Browser executable to launch an external preview. If this value is `null` it'll use the system default. Defaults to discovered location of Chrome or FireFox if installed, otherwise `null`.

#### OpenFolderCommand
Determines the executable used to open a folder or folder file location in Windows. Defaults to `Explorer.exe` but can be any other Explorer replacement shell you use.

#### TerminalCommand and TerminalCommandArgs
The **TerminalCommand** is the command interpreter used which defaults to **Powershell**. The arguments are the stock arguments to open the shell in a specific folder.

**Powershell**

```json
  "TerminalCommand": "powershell.exe",
  "TerminalCommandArgs": "-noexit -command \"cd '{0}'\"",
```

**Command**

```json
  "TerminalCommand": "cmd.exe",
  "TerminalCommandArgs": "/k cd /D \"{0}\"",
```