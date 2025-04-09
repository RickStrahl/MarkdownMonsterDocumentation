When you install Markdown Monster the installation folder is added to your current User path. To start Markdown Monster from the command line you can do:

```powershell
markdownmonster readme.md
```

or simply:

```powershell
mm readme.md
```

#### Multiple Files
Markdown Monster can also open multiple files by passing multiple filename parameters to the application:

```powershell
mm readme.md todo.md changelog.md
```

#### Opening Folders
You can also open a folder in the [FolderBrowser](VFPS://Topic/_4WU1CJYKA) by specifying a folder name from the command line:

```powershell
mm .
mm .\dev\MyPoject
```

You can combine both opening a file and folder in the FolderBrowser like this:

```powershell
mm . readme.md
mm c:\temp c:\temp\SampleMarkdown.md
```

#### Path Support
Markdown Monster automatically figures out the current path and opens files referenced with relative paths as well as full paths. 

All of the following work:

```powershell
mm .\docs\Readme.md
mm ..\Config.md
mm c:\docs\Readme.md
```

### Line Number
You can also specify a line number to open the document on using the `-line 100` command line switch:

```powershell
mm .\docs\Readme.md -line 100
```

### Open a new Empty Document
To open an empty document pass `untitled`:

```powershell
mm untitled
```

### Open a new Document with Pre-filled Text
To open a new untitled document with text preset you can use one of the following syntax:

```text
untitled.<encoding>,<encodedContent>
```

Encodings are:

* **base64** - base64 encoded string - recommended approach
* **urlencoded** - a UrlEncoded string
* **json** - single line JSON string with or without quotes
* **text** - plain text - recommended only for very simple one liners

In actual shell commands this looks like this:

```powershell
mm untitled.base64,IyBIZWxsbyBXb3JsZAoKSXQncyBhICoqY3J1ZWwsIGNydWVsKiogd29ybGQu
mm untitled.urlencoded,This%20is%20a%20test.
mm "untitled.text,This is a new document"
mm "untitled.json,'This is\nmulti-line content.'"
```

> **Note:** If you are using `text` or `json` make sure that the entire parameter is wrapped into quotes as spaces and quotes will break the OS command line parsing. Even so you may still run into issue with `"` quotes **inside of the text**. For this reason we recommend you use `base64` or `urlencoded`.

### Open a Document with Pre-Filled Text from Base64 Data
If you need to open a new document with a large amount of multi-line text, using base64 is the preferred mechanism and there's an explicit `-base64text` command line parameter to do it:

```powershell
mm -base64text IyBIZWxsbyBXb3JsZAoKSXQncyBhICoqY3J1ZWwsIGNydWVsKiogd29ybGQu
```

### Other File Formats Supported
Markdown Monster also supports a ton of other file formats with Syntax Highlighting including:

csharp, html, css, javascript, typescript, xml, config, powershell, foxpro, yaml, dockerfile and many more. 

For a complete list check the `EditorExtensionMappings` key in **Tools -> Settings**.

### Additional Command Line Options
There are a number of additional Command Line Operations available that let you configure Markdown Monster. Please see the [Command Line Operations](VFPS://Topic/_5FP0XP68P) topic for details.