Markdown Monster installs a  `markdownmonster:` **Application Protocol Handler** (also referenced as a **Uri Scheme** in Windows Documentation), which allows you to open Markdown Monster documents from within a Web Browser via a URL or using `ShellExecute` on Windows. Using the Protocol Handler URL you can:

* Open an existing file
* Open an empty document
* Open a new document with pre-set text <small>(in a number of ways)</small>

![](https://github.com/RickStrahl/ImageDrop/raw/master/MarkdownMonster/MarkdownMonsterProtocolHandler.gif)

### What's a Protocol Handler?
A **Protocol Handler** is an OS registered URL 'prefix' - specifically `markdownmonster:` - that Web browsers and the Shell recognize as belonging to Markdown Monster. In a browser when a `markdownmonster:` URL is detected the browser prompts for permission to launch Markdown Monster and then executes the specified command. With these URL *monikers* you can open Markdown Monster from a Web Browser or any other application that can invoke a Web link.

> #### @icon-info-circle Application Protocol Handler Size is Limited to 2040 Characters
> Application Protocol Handlers invoked from a Web Browser are **limited in length to 2040 characters** of the URL moniker passed which means you unfortunately cannot use it for passing very large documents from a browser to MM. You can however use relatively small Markdown blocks and open new documents quite nicely. For larger blocks an optional Web Server is available in Markdown Monster.

> #### @icon-warning Protocol Handlers require a Full Installation
> Because Protocol Handlers have to be installed in the Administrative area of the registry, URL Monikers are only configured using the **full Markdown Monster installation program**. The Portable installer and application startup configuration cannot register URL Monikers. If you change location of MM, you'll need to re-run the full setup to re-register the `markdownmonster:` URL Moniker.

### Trying it out
One simple way to try out a URL moniker is via the Web Browser address bar. Simply type a moniker into the address bar and it executes.

Try using this to open a new document:

```text
markdownmonster:untitled
```

or this to open a document with some pre-set text:

```text
markdownmonster:untitled.text,Hello cruel world
```

<small>(note in this example the browser automatically URL encodes the string)</small>

More commonly you'll want to encode your text though using either `markdownmonster:untitled.urlencode` for single line text, or more likely `markdownmonster:untitled.base64`. Here's what the Url encoded version looks like:

![](/images/UrlMonikerInAddressBar.png)

When you use a Protocol Handler in the browser, the browser pops up a verification dialog to ensure that your users want to launch the external application. 

![](/images/UrlMonikerAuthorizationDialog.png)

If you consent, Markdown Monster is started - in this case with a new document with some pre-filled 'Hello World' text.

### Available Operations

#### Open existing Files or Folders
You can open existing files by using a URL like this:
```powershell
markdownmonster:c:\temp\test.md
```

You can also use a path instead to open a folder in the folder browser:

```powershell
markdownmonster:c:\temp
```

> Note: Most browsers automatically fix up non-Url Encoded filenames. But if you are programmatically using URL Monikers we recommend you still explicitly URL encode any paths you provide.

#### Open a New Empty Document
You can also open new documents using the special `untitled` command which allows you to create an empty or pre-filled  document.

To open an empty document:

```powershell
markdownmonster:untitled
```

#### Open New Documents with Pre-Filled Text
To open a document with pre-filled text you can the following syntax:

```
markdownmonster:untitled.<format>,<content>
```

This syntax is a bit cryptic but it allows you to encode the data in a variety of ways. Supported formats are:

* base64
* urlencoded
* json
* text

Examples:

```
markdownmonster:untitled.base64,VGhpcyBpcyBhIHRlc3Qgc3RyaW5nIG9mIHRleHQu
markdownmonster:untitled.text,This is a new document
markdownmonster:untitled,json,'This is\nmulti-line content.'
markdownmonster:untitled.urlencoded,This%20is%20a%20test.
```

> #### @icon-info-circle Use base64 for new Documents if possible
> We recommend that you use base64 if possible as it provides the cleanest way to represent text as a single URL embeddable string. Note that JavaScript has `atob()` and `btoa()` functions respectively to create base64 content in the browser if you need to programmatically create and add content to urls in Web applications.

### Using Protocol Handlers in a Web Page
So how practical are protocol handlers? This protocol helper obviously only works **if Markdown Monster is installed**. Unfortunately there's no good way to determine from within a Web page whether a protocol handler is available - the only way to know whether it's installed or not is when it fails.

But, if you're building an internal application where you know people might have Markdown Monster to edit text, you can easily hook it up into pages via links or some very simple script code.


#### Linking
The easiest way to open Markdown Monster via Protocol Handler is by using standard `<a href>` links. 

**Open a new Document**
  
```html  
<a href="markdownmonster:untitled.urlencoded,Hello+World">Open in Markdown Monster</a>
```

**Open a file (you have to know what the path is)**

```html  
<a href="markdownmonster:c:\temp\test.md">Open in Markdown Monster</a>
```

#### Using `<script>` Code
You can also open a Markdown Monster with dynamically created text. 




* **Type into the Browser Address Bar**  
Just type in the URL: `markdownmonster:c:\temp\test.md` etc.

* **Use ShellExecute in any Application**  
Any application that can use `ShellExecute()` to 'execute' URLs can create this Markdown Monster URL Moniker. In .NET you can use `Process.Start()` which has options to process a Web URL.

### Using JavaScript code to open Markdown Monster

```html

<textarea id="MarkdownText" class="markdowntext form-control" rows="15" placeholder="Enter some Markdown text">
#Markdown Text

Change me! **No Really!**
</textarea>


<button id="btnOpenInMarkdownMonster" class="btn btn-primary mt-2" onclick="openInMm()">
    <img src="images/MarkdownMonster_Icon_32.png" style="height: 20px;margin-right: 10px" />
    Open in Markdown Monster</button>
<script>
    function openInMm() {
        var text = document.getElementById("MarkdownText").value;        
        var b64 = btoa(text); 
        
        // IMPORTANT: Url length is limited to 2048 characters
        var url = "markdownmonster:untitled.base64," + b64
        console.log(url.length,url);
        
        if(url.length > 2048)
        {
            alert(
                "The length of the encoded document that can be edited externally is limited to 2048 characters.\n\n" + 
                "Length of this encoded text: " + url.length);
            return;
        }
        
        // navigate
        window.location.href = url;
</script>
```

### More Info on Protocol Handlers
If you want to understand more technical detail about what you can and can't do with Protocol Handlers check out Eric Lawrence's comprehensive post on the subject:

* [Web-to-App Communication: App Protocols](Web-to-App Communication: App Protocols)