You can integrate Markdown Monster with external applications in several ways:

* Open a document via command line (`mm "c:\path\filename.md"`)
* Close an open document via command line (`mm -close "c:\path\filename.md"`) 
* Create a 'temporary document' with an `*_autosave.md` postfix

### Opening Documents from the Command Line
It's easy to open Markdown Monster document from the command line simply by passing path to a document to the main executable. There are two ways to invoke Markdown Monster via script or process launchers and load a file:

```dos
mm "c:\temp\filename"
```

or using the full executable:

```dos
markdownmonster "c:\temp\filename"
```

`markdownmonster.exe` and the `mm.exe` passthrough alias are the main executables you can do to lauch Markdown and other supported files from the commandline. These executables are **added to your user path during installation** so there's no need to provide a path for the exe's.

Note that you can provide multiple files to open on a single command line operation.

### Closing Documents from the Command Line
If you want to automate the process of editing documents in Markdown Monster, you may also find it useful to close a document once you are done with Markdown Monster when you return to some other application or process that initially opened the document. 

This allows you to 'clean up' the Markdown Monster instance and pick up the modified content from the saved file.

To close a document:

```dos
mm -close "c:\temp\filename"
```

The order is siginificant - the `-close` has to proceed the filename and you can specify multiple `-close` \ filename combinations.

### `-autosave` Command Line Option
If you specify any file names on the command line, you can optionally force files to be saved as soon as you are editing the text using the `-autosave` command line option. This flag is applied to any files you open via the command line which means files are written to disk as soon as you stop typing. This allows any external applications that might be monitoring the specified file to pick up changes as quickly as they are saved in MM.

```dos
mm "c:\temp\filename" -autosave
```

### Opening Markdown Monster in a Browser or with ShellExecute (Application Protocols)
If you're using Markdown Monster in a browser you can also use a URL to open Markdown Monster. For example, the following link can be used to force MM to open with an empty document:

```html
markdownmonster:untitled
```

You can also open a new document with preset text:

```html
markdownmonster:untitled.text,Hello Cruel World
```

or - if the text is more complex and includes line breaks and other extended text you can use base64:

```html
markdownmonster:untitled.base64,VGhpcyBpcyBhIHRlc3Qgc3RyaW5nIG9mIHRleHQu
```

There are more options available for Application Protocols:  
[Open from Browser with Application Protocols](VFPS://Topic/_5RJ1CKNRJ)