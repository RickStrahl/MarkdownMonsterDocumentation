The slide out Folder Browser allows you quickly browse, open and manipulate files and folders in the Windows file system.

To access the Folder Browser use the **@icon-files-o icon** on the toolbar on the right, or in the Window control box at the top left of the main window. You can also use a keyboard shortcut: **Alt-a-f**.

Control and to create a new document because in here there's some text that I wanna copy right and I wanna paste that into another topic so I
Here's what the Folder Browser looks like:

![](/images/folderbrowser.png)


### Opening Folders
There are a number of ways to open a folder for the folder browser:

* Type a folder name into the Textbox above the list
* Click the  @icon-ellipsis-h icon to pick a folder
* Click the @icon-location-arrow icon top open the active document's parent folder

### Opening Files
You can **double click** or **press Enter** on any file to open it. If the format is one that Markdown Monster knows how to work with the document is opened in the editor. You can also simply drag a file into the editor window and it will open there if has one of the supported file extensions

### Images
You can preview images clicking and displaying them in the Editor view. Images are read-only when displayed but the context menu allows you to open images in an image viewer or editor (configurable in Settings). Images can be viewed or edited using **Show Image** or **Edit Image** and you can **drag images** images into an open Markdown document to create an image reference in the document.

Images are opened in the configured image editor (set via the **ImageEditor** configuration setting). jpg, png, and gif images are supported for this operation.

### Unsupported Files
All other files are sent to the standard Shell mapping and displayed in the configured viewer. Executable files are not allowed to be executed.

### File Management
The short cut menu in the TreeView allows access to the following file operations:

* Create a new File or Folder
* Rename an existing file
* Delete a file

### Open Terminal or Explorer
You can also open a Command prompt or Explorer window at the selected file location. Terminal uses the **TerminalCommand** and **TerminalCommandArgs** configuration settings to start a command prompt. The Explorer link simply opens the Windows File Explorer in the specified location.

### Find Files
There are three ways you can find files in the Folder Browser:

* Type into the list to jump to closest match
* Use the **Search Box** above the list
* Use Find in Files

The first two options search the currently visible tree and subtree. Find in files searches the entire subtree for files including contained content optionally.

For more information see the Finding Files topic.

### Active Folder Navigation
By default the folder browser opens at its last remembered location and stays there unless you explicitly navigate to a new location. You can use the Arrow icon in the toolbar to navigate to the current document's location quickly. There are also menu options on the View Menu to activate the Folder Browser, and the Tab Context menu to show the folder browser for the active document.

Alternately you can change the folder explicitly by using the folder selection box at the top of the list.

### Syncing Document and Folder Browser
Some people prefer to keep the Folder Browser **always in sync with the active document**. You can do this via the Transfer icon on the menu bar, or a configuration settings in the Settings. When toggled on, whenever you change the active document, the folder browser immediately navigates to that folder and selects that file in the folder browser. 

The default for this setting is off as this constant navigation can be distracting, so you have to explicitly enable it. The setting is sticky, so it's remembered across sessions.

### Commit to Git and Push
You can also optionally commit the selected file to Git. If selected the current file only is committed and optionally pushed to the server, depending on the `GitCommandBehavior` setting (`CommitAndPublish` or `Commit`)

### File Icons
The browser automatically displays icons for most common types of files.

You can optionally disable this feature by setting `FolderBrowser.ShowIcons: false` in the configuration file. Turning off icons can make the file browser run faster.

You can also add icons for other file formats by adding a 32x32 PNG file with the extension name into the `Editor\fileicons` folder.