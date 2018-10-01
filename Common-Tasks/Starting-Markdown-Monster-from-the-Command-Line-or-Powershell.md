When you install Markdown Monster the installation folder is added to your current User path. To start Markdown Monster from the command line you can do:

```dos
markdownmonster readme.md
```

or simply:

```dos
mm readme.md
```

#### Multiple Files
Markdown Monster can also open multiple files by passing multiple filename parameters to the application:

```dos
mm readme.md todo.md changelog.md
```

#### Opening Folders
You can also open a folder in the [FolderBrowser](VFPS://Topic/_4WU1CJYKA) by specifying a folder name from the command line:

```dos
mm .
mm .\dev\MyPoject
```

You can combine both opening a file and folder in the FolderBrowser like this:

```dos
mm . readme.md
mm c:\temp c:\temp\SampleMarkdown.md
```

#### Path Support
Markdown Monster automatically figures out the current path and opens files referenced with relative paths as well as full paths. 

All of the following work:

```dos
mm .\docs\Readme.md
mm ..\Config.md
mm c:\docs\Readme.md
```

### Other Formats Supported
Markdown Monster also supports a ton of other file formats with Syntax Highlighting including:

csharp, html, css, javascript, typescript, xml, config, powershell, foxpro, yaml, dockerfile and many more. 

For a complete list check the `EditorExtensionMappings` key in **Tools -> Settings**.

### Configuration Commands
There are two additional commands that are used to clean up Markdown Monster's configuration settings.

```dos
mm reset
```

This command resets all of Markdown Monster's configuration settings in `markdownmonster.json` and removes all Addins installed. Use this option to reset MM if settings somehow have become corrupt.

> #### @icon-warning Use with Care
> Resetting all settings will remove all stored settings and preferences, so be careful with resetting if you've customized many settings explicitly. You can also reset configuration settings by simply renaming:
>
> `%appsettings%\Markdown Monster\markdownmonster.json` 
>
> file after shutting down MM.

```dos
mm uninstall
```

This command removes all non-local settings that are made when installing Markdown Monster. This includes various registry entries.
