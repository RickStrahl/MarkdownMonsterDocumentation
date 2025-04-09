Sometimes you need to access an external program to view a file or perform additional tasks beyond what Markdown Monster can provide. Perhaps you need some advanced text editing that MM doesn't provide, or perhaps you want to use a custom image editor to quickly edit an image file.

There are a couple of ways you can access external programs and optionally reference the currently open or selected file:

* Standard **Open With...** Shell Functionality
* Adding your own **External Programs**

Both of these are available on:

* The Editor and Tab Context Menus via **Open...**
* The Folder Browser's File or Folder Context Menu via **Open...**

## Standard Open With... Behavior
The **Open With** functionality uses the standard Windows **Open With...** dialog that based on a file name shows associated applications that Windows knows about:

![](/images/FolderBrowser_OpenWith_Dialog.jpg)

This option is available via:

* Active Document Context Menu
* Active Tab Context Menu
* Folder Browser Context Menu

Here's how you get to the option on the context menu (Folder Browser Version):

![](/images/FolderBrowser_OpenWith.png)


## Custom External Programs
In addition to the default Windows behavior you can also **add your own External Programs** and show them on the **Open With** context menu, just below the default **Open...** menu option.

![](/images/FolderBrowser_ExternalPrograms.png)

> If VS Code or Paint.NET are installed on your machine they are automatically added to your Open list the first time MM is installed.

### Configuring External Programs
External Programs have to be configured **manually** in the `MarkdownMonster.json` file, by specifying an array of external programs in the JSON file.  You can access this file via the menu:

* Tools -> Settings
* Search for **External Programs**
* Click the link button to edit in `markdownmonster.json`

> #### @icon-warning External Editing of MarkdownMonster.json
> If you make changes to `MarkdownMonster.json` outside of the Markdown Monster editor, make sure that Markdown Monster is **not running** before saving. Otherwise MM will overwrite your changes before they are used. Using the internal editor detects changes to the configuration file and reloads the configuration settings upon save, so changes are preserved.

Here's what the `ExternalPrograms` configuration in `markdownmonster.json` looks like with some examples:

```json
"ExternalPrograms": [
  {
    "Name": "Open in VS Code",
    "Executable": "C:\\Program Files\\Microsoft VS Code\\Code.exe",
    "Args": "\"{0}:{1}:{2}\" -g",
    "SaveBeforeActivation": true,
    "Extensions": "TEXT,FOLDER"
  },
  {
    "Name": "Open in Paint.NET",
    "Executable": "C:\\Program Files\\paint.net\\paintdotnet.exe",
    "Args": "{0}",
    "Extensions": "IMAGE"
  },
  {
	"Name": "Open in SmartGit",
    "Executable": "C:\\Program Files\\SmartGit\\bin\\smartgit.exe",
    "SaveBeforeActivation": false,
    "Args": "{0}",
    "Extensions": ""
  },
  {
    "Name": "Open in Online SVG Editor 2",
    "Executable": "https://mediamodifier.com/svg-editor",
    "Args": "{ToClipboardText}",
    "SaveBeforeActivation": false,
    "Extensions": ".svg"
  }
],
```

`ExternalPrograms` is the top level array that holds a list of programs. MM Adds a VS Code and Paint.NET if they are available by default.

Each program specifies a number of parameters:

* **Name**  
This is the display name of the program that is displayed in the Context menu

* **Executable**  
The **full path to the executable** that is to be launched. The file has to exist.
Can also be an **HTTP Url** to open a Web site.
   
   > Both **Executable** and **Args** expand embedded system environment variables using `%variable%` syntax.

* **Args**  
Command line arguments to pass to the application. There are a number of expansions that can be used

   * `{0}`  -  Current selected item, the active file or the folder browser selection
   * `{1}`  -  Current Line Number - only applies for the Active Document Context Menu
   * `{2}`  -  Current Cursor Column - only applies to the Active Document Context Menu
   * `{CurrentFile}` - Explicitly specifies the current file
   * `{CurrentFolder}` - Explicitly specifies the current folder
   * `{ToClipBoardText}` - If specified adds file content to the clipboard.  If the document in the editor is opened via the Editor context menus, the current document text is used. If selecting a file in the Folder Browser, the content of any text file from disk is used. This feature is useful when the external application doesn't support a file name via arguments, and it's often useful with URLs where you can later paste content into a form/page.
   
* **Extensions**  
The Extensions list is a filter that determines whether the program is available for a given file or folder. You can optionally specify a comma delimited list of file extensions that this program can be applied to. 

   To specify a list of extensions you can use: `.md,.mkdown,.txt`  
  
   In addition you can also use several special parameters you can specify in addition to extensions:
     * **TEXT**  - Any Text files
     * **IMAGE** - Any Image Files
     * **FOLDER** - Any folders

   You can add one or more external programs that can be run from the active document in the editor or the selected file or folder in the folder browser.

  If you leave the extension list empty, the program **is always shown** on the **Open With...** list.

* **SaveBeforeActivation**  
If `true` saves the active document before activation when using on the active document **without prompting**. The default behavior on a dirty document prompts you to save - with this flag set to `true` the file is immediately saved. Note that `Untitled` documents always prompt to save the file first and if you don't save, edit a temporary file that is deleted.

> #### @icon-info-circle Dedicated Image Viewer and Editor
> Note that MM has a configuration for **dedicated image viewer and image editor** which is configured separately in the MM configuration. These values - if set - are used for the **View Image** and **Edit Image** options in various menus to preview and edit images externally. The configuration settings for this are found here or in the `markdownmonster.json` configuration file:
> 
>  ![](/images/ImageEditorConfiguration.png)
> 
> which should be your preferred way for configuring your primary image editor. External Programs allow you to add additional image editors should you need more variety for different editing/viewing scenarios.