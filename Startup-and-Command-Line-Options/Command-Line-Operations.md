In addition to [opening files and folders from the command line](VFPS://Topic/_4X313DNEU) you can also perform a few operational tasks using Markdown Monster's Command Line Interface.

There are three sets of commands:

* Editor UI commands using `mm.exe` or `markdownmonster.exe`
* Operational CLI Commands using `mmcli.exe`

> #### @icon-info-circle Available on the Windows Path
> All `markdownmonster`, `mm` and `mmcli` are all available on the **Windows Path** by default, as they have been added to the User path during installation or 1st startup.

> #### @icon-info-circle Launching Markdown Monster from WSL
> You can also launch Markdown Monster from Windows Subsystem for Linux (WSL) by using the full executable names: `mm.exe`, `markdownmonster.exe` or `mmcli.exe`. For example, to open `README.md` from a local WSL folder use: `mm.exe README.md`. Note that unlike on Windows the `.exe` extension is **required**.

### Editor UI Commands - mm.exe
The following commands are command line switches that affect the behavior and startup of Markdown Monster's UI. They are fired using either `mm.exe` or `markdownmonster.exe` which can be used interchangeably.

+----------------------+----------------------------------------------------------------------------------------------------------+
| Command/Arguments    | Function                                                                                                 |
+======================+==========================================================================================================+
| **-line**            | Line number when opening a document <br/>`mm .\readme.md -line 100`\                                     |
|                      | **Tip**: you can also use `c:\temp\readme.md:5` to specify a line number                                 |
+----------------------+----------------------------------------------------------------------------------------------------------+
| **-presentation**    | Flag that starts Markdown Monster in **Presentation Mode**\                                              |
|                      | `mm -presentation`                                                                                       |
+----------------------+----------------------------------------------------------------------------------------------------------+
| **-newwindow**       | Flag that forces a new Window to be opened regardless of the `SingleInstance` configuration Setting\     |
|                      | `mm .\doc.md -newwindow`                                                                                 |
+----------------------+----------------------------------------------------------------------------------------------------------+
| **-nosplash**        | When specified won't show the splash screen.<br/>`mm -nosplash`                                          |
+----------------------+----------------------------------------------------------------------------------------------------------+
| **-delay**           | When specified loads Markdown Monster with a delay. Used for updates.<br/>`mm -delay`                    |
+----------------------+----------------------------------------------------------------------------------------------------------+
| **-close**\          | Closes a file that is open in the editor if found<br/>                                                   |
| fileName             | `mm -close "c:\temp\MyDocument.md"`                                                                      |
+----------------------+----------------------------------------------------------------------------------------------------------+
| **-autosave**\       | When set forces the document(s) opened from the command line to auto-save after any typing operation.    |
| fileName             | `mm "c:\temp\MyDocument.md" -autosave`                                                                   |
+----------------------+----------------------------------------------------------------------------------------------------------+
| **-stdin**           | Read content from StdIn using pipe command. Opens a new 'untitled' document.\                            |
|                      | `DIR | markdownmonster -stdin`                                                                           |
+----------------------+----------------------------------------------------------------------------------------------------------+
| **-base64text**\     | Opens a new 'untitled' document with the base 64 decoded text inside of it.\                             |
| base64Text           | `mm -base64text VGhpcyBpcyBhIHRlc3Qgc3RyaW5nIG9mIHRleHQu`                                                |
+----------------------+----------------------------------------------------------------------------------------------------------+
| **-startwebserver**  | Starts the MM internal Web Server for various remote operations\                                         |
|                      | `mm -startwebserver`                                                                                     |
+----------------------+----------------------------------------------------------------------------------------------------------+
| **-stopwebserver**   | Stops the MM internal Web Server\                                                                        |
|                      | `mm -stopwebserver`                                                                                      |
+----------------------+----------------------------------------------------------------------------------------------------------+
| **-runtimeinstall**  | Checks to see if the .NET Desktop Runtime is installed and if not offers to install it.\                 |
|                      | `mm -runtimeinstall`                                                                                     |
+----------------------+----------------------------------------------------------------------------------------------------------+

#### -line
This parameter allows you to open a file on a given line. The `-line` parameter is only applied to the first file. 

Alternately you can also use the new syntax of `filename.md:11` where the line number is directly appended to the filename via `:lineNo`. You can [apply this syntax to multiple files](https://raw.githubusercontent.com/RickStrahl/ImageDrop/master/MarkdownMonster/OpenMultipleFilesAtLine.gif). 

#### -presentation Mode
If you want to start Markdown Monster in presentation mode that shows the preview as a maximized view, use the `-presentation` switch. This view doesn't show the editor initially although you switch into regular editing mode. You can use this switch in addition to optional files you want to open.

`mm .\README.md -presentationmode` or `mm -presentationmode`

#### -newwindow
This flag forces a new Markdown Monster window to be opened with the selected file(s) or folder to be opened, rather than opening the document in the current instance. This setting forces a new window even if the `SingleInstance` configuration setting is set to `true`. This is used internally for **Open in New Window**, but useful anytime when you want to open side by side windows. You can use this switch 

`mm .\README.md -newwindow` or `mm -nosplash`

#### -nosplash
When specified causes the startup splash screen to not be displayed. Same as the `DisableSplashScreen` configuration switch, except it's a one time operation that applies only to the current launch operation.

`mm .\README.md -nosplash`  or `mm -nosplash`

#### -delay
Delays loading Markdown Monster during startup. Used internally when Markdown Monster is restarted for theme updates and other settings that require a restart. Delay is approximately 1.5 seconds.

`mm .\README.md -delay`

#### -autosave 
If this switch is specified when passing in one or more filenames for opening, the files are opened in auto-save mode, which means any changes are written to disk whenever the user stops typing for a brief moment. This can be useful for external applications that want to use Markdown Monster for editing and detect changes in the editor immediately.

`mm .\README.md -autosave`

#### -close Filename Command
This option allows you to close an already open file in the editor. If you have multiple tabs open the tab is closed and if the last tab is closed Markdown Monster is shut down. This can be useful for external applications that might want to open Markdown Monster for external Markdown editing, capture output saved to disk perhaps with the `-autosave` switch, and then close the opened editor window.

`mm .\README.md -close`

#### -stdin
This option allows you to capture StdIn input from another application and open the captured text in Markdown Monster as a new document. For this to work you can **pipe** the content of another console application into Markdown Monster using the **Windows Pipe Command**.

Example 2:

```ps
DIR | markdownmonster -stdin
```

#### -base64text
This option creates a new, 'Untitled' document and sets the initial text to -base64text.

```powershell
mm -base64text IyBIZWxsbyBXb3JsZAoKSXQncyBhICoqY3J1ZWwsIGNydWVsKiogd29ybGQu
```

#### -startwebserver / -stopwebserver
These commands allow you to start and stop the [MM internal Web server](dm-topic://_5S1009YX1) which can be used to remotely open and access documents.

```powershell
mm -startwebserver

mm -stopwebserver
```

#### -runtimeinstall
Checks to see if the .NET Desktop Runtime required to run Markdown Monster is installed on the machine. If it isn't you are prompted to download it and install it. Optionally use `-silent` switch to avoid prompts and *'just do it'*.

```powershell
mm -runtimeinstall
```

### CLI Commands - mmcli.exe
The following commands use a separate `mmcli.exe` to perform a number of useful automated operations using Markdown Monster's functionality.

+------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Command                      | Function                                                                                                                                                                                     |
+==============================+==============================================================================================================================================================================================+
| **version**                  | Displays Markdown Monster Version.<br/>                                                                                                                                                      |
|                              | `mmcli version`                                                                                                                                                                              |
+------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **reset**                    | Resets Markdown Monster to its default settings.<br/>                                                                                                                                        |
|                              | `mmcli reset`                                                                                                                                                                                |
+------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **errors**                   | Display the Markdown Monster Error Log in the default text editor.<br/>                                                                                                                      |
|                              | `mmcli errors`                                                                                                                                                                               |
+------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **clear-errors**             | Clears the Markdown Monster Error Log.<br/>                                                                                                                                                  |
|                              | `mmcli clear-errors`                                                                                                                                                                         |
+------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **uninstall**                | Removes all Markdown Monster machine settings. Run after you've shut down all Markdown Monster                                                                                               |
|                              | instances.<br/>                                                                                                                                                                              |
|                              | `mmcli uninstall`                                                                                                                                                                            |
+------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **install-webview**          | Runs the WebView control installer that installs the WebView runtime required to run Markdown Monster                                                                                        |
+------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **cleanup-webview**          | Removes the WebView Environment Folder created when Markdown Monster runs. This folder holds the separate, application specific browser environment settings while running Markdown Monster. |
+------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **setportable**              | Sets portable mode where settings are stored in the install folder<br/>                                                                                                                      |
|                              | `mmcli setportable`                                                                                                                                                                          |
+------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **unsetportable**            | Sets back to desktop mode with config settings to `%appdata`.<br/>                                                                                                                           |
|                              | `mmcli unsetportable`                                                                                                                                                                        |
+------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **enable-windows-longpaths** | Enables Windows Long Path support. This is a **global** Windows  setting that affects all applications *(requires elevated rights)*.<br/>                                                    |
|                              | `mmcli enable-windows-longpaths`<br/>                                                                                                                                                        |
|                              | `mmcli disable-windows-longpaths`                                                                                                                                                            |
+------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **register**                 | Registers Markdown Monster installation.<br/>                                                                                                                                                |
|                              | `mmcli register licenseSerial registerEmail`                                                                                                                                                 |
+------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **markdowntohtml**           | Converts Markdown documents to HTML.<br/>                                                                                                                                                    |
|                              | `mmcli markdowntohtml -i "c:\temp\doc.md" -o "c:\temp\doc.html" --theme Dharkan --rendermode packagedhtml`                                                                                   |
+------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **htmltomarkdown**           | Converts an HTML document to Markdown.<br/>                                                                                                                                                  |
|                              | `mmcli htmltomarkdown -i "c:\temp\doc.html" -o "c:\temp\doc.md" -open`                                                                                                                       |
+------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **markdowntopdf**            | Converts a Markdown document to a PDF file.<br/>                                                                                                                                             |
|                              | `mmcli markdowntopdf -i "c:\temp\doc.md" -o "c:\temp\doc.pdf" --theme Github --page-size A4`                                                                                                 |
+------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
+------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+



#### version
Displays the Markdown Monster version in the console window.

`mmcli version`

#### reset
The reset operation resets all of Markdown Monster's settings back to its defaults by creating a new `MarkdownMonster.json` file. The reset command also creates a backup file in the same folder that you can compare against.

`mmcli reset`

#### uninstall
The uninstall option removes all the machine specific settings from the registry so you end up with a clean machine. This command is primarily intended for portable installs, which although it runs portably in a self-contained folder (if permissions allow), will write a few things like file associations and pathing into the registry. The `uninstall` command removes only those settings.

**Uninstall does not remove any files or folders.** If you are running a machine wide installation settings are stored in `%appdata%\Markdown Monster` and if you are sure you want to completely remove Markdown Monster you can delete this folder manually - the uninstall will not touch this folder.

`mmcli uninstall`

> #### @icon-info-circle Full Version Uninstall: Use the full Uninstaller
> If you installed the full version of Markdown Monster using the Installer it's recommended you run the full Uninstall through Programs and Features or by running the `Uninstall.exe` in the install folder.
>
> The full uninstall removes the same settings as the `uninstall` switch but also removes files, folders and the shortcuts it created.

#### install-webview
Markdown Monster relies on the Chromium WebView2 control in order to run. The installation automatically installs the WebView if it's not found. If for some reason the WebView gets uninstalled after installation you can run this command to get the WebView2 Runtime reinstalled.

#### cleanup-environment
Markdown Monster creates its own private WebView environment that's separate from the machine global WebView profile, so there's no overlap of settings. MM only browses local content with the WebView, but nevertheless the browsing environment is completely separate from the system profile. This command removes the stored, cross- session browser environment. 

#### setportable / unsetportable
These two settings toggle between portable and full desktop install. The primary differences between a portable install and a full install is the location of the settings folder. The portable install tries to create a `.\PortableSettings` folder in the install directory and keep all settings local to that install. A portable install can be installed simply by copying files from a zip file.

However, in order for a portable install to work you have to make sure you use a folder that has write permissions to allow configuration settings to be updated in this folder.

`setportable` allows you to switch a full install into portable mode by creating a `_IsPortable` file and creating the local `.\PortableSettings` folder if permissions allow. If permissions fail, MM will use the standard `%appdata%\Markdown Monster` location the full install uses.

`unsetportable` simply removes the `_IsPortable` file which makes Markdown Monster use the default `%appdata%\Markdown Monster` folder for all settings and addins.

#### register
This option lets you register Markdown Monster via the command line.

To register you need to provide the License Serial number and the email address that was used when purchasing a license (you can find the email on your order confirmation).

`mmcli register <licenseSerial> <email>`

#### markdowntohtml
This allows you convert a markdown document to HTML using the following syntax:

```ps
mmcli markdowntohtml -i "<markdownFile>" -o "<htmlFile>"
      --rendermode [html|fragment|packagedhtml|zip]
      --theme [<anyAvailableTheme>]
      -open
```

You pass the input markdown and output HTML file to generate. If you skip either of these you'll be prompted. The `--open` parameter opens the document in Markdown Monster via `mm "<htmlfile>"` .

The `renderMode` is one of the following:

* **html** - Html document with Preview Theme wrapper document (default)
* **fragment** - Just the raw Html fragment without a wrapping PreviewTheme document
* **packagedhtml** - single, large HTML document with all dependencies embedded as inline resources
* **htmlfiles** - Html document with dependencies in the output file folder
* **zip** - Html document and dependencies packaged into a Zip file

Note that all options except `fragment` render a complete HTML document using the current **PreviewTheme** configured, unless you override the `--theme` parameter where you can specify any of the installed themes.

The `-open` flag if present opens the document in the browser after completion.

#### htmltomarkdown
This allows you to convert HTML documents to Markdown using the same mechanism as **Paste Html** in the Markdown Monster editor view. The command line for this looks like this:

```ps
mmcli htmltomarkdown -i "<inputHtmlFile>" -o "<outputMarkdownFile>" -open
```

You pass an HTML file as input and a Markdown document as output. If files aren't provided MM prompts for file names. The `-open` flag opens the Markdown document in Markdown Monster after generation.

#### MarkdownToPdf
This option allows you to print a Markdown document into a PDF file.

```ps
mmcli markdowntopdf -i "<inputMarkdownFile>" -o "outputPdfFile" -open
      --theme [<anyAvailableTheme>]  
      --orientation [Portrait|Landscape]
      --page-size [Letter|Legal|A4|B4]
```