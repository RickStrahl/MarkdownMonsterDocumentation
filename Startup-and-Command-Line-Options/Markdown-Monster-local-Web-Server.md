Markdown Monster includes an optional local HTTP server that can be used to launch Markdown Monster with preset content remotely, when the server is running. The server has to be started in order for this to work, although you can request starting the server in a number of manual and automated ways.

The following demonstrates some of the external operation with an HTTP REST Client ([WebSurge](https://websurge.west-wind.com))

![Markdown Monster internal Web Server Interaction](https://raw.githubusercontent.com/RickStrahl/ImageDrop/refs/heads/master/MarkdownMonster/WebServerAutomation.gif)

Using the Web Server you can remotely:

* Open a new Document with content text
* Open a new Empty document
* Open a document from a path
* Retrieve the contents of the active document

By default the Web Server **is not enabled** and you have to start it. To start the Markdown Monster Web Server you can do one of the following:

* Toggle the `Tools -> Web Server` menu checkbox configuration setting on
* Set the `WebServer.IsRunning=true` configuration flag
* Set the `WebServer.AutoStart=true` configuration flag to auto-start the server on startup
* Run `mm -startwebserver` from the Terminal to explicitly start the server
* Use the `markdownmonster:webserver` Web Protocol Handler from browser or shell (toggles)

Once the server is running you can open and retrieve open document text in Markdown Monster from a Web Browser via HTTP requests. Opening text in a new document in Markdown Monster can be triggered via a relatively simple fetch script that is provided as a sample.

> #### @icon-info-circle Web Sample Page and Support JavaScript Library
> An example of what you can do with the Protocol Handler and Web Server to automate Markdown Monster from a browser, you can look at the examples in `/SampleDocuments/BrowserIntegration`. A library that helps with integration operations can be found in `markdownmonster-integration.js`.

> #### @icon-lock Security?
> The Web Server Markdown Monster uses is a local only Web Server, so security issues at most are limited to the local machine. Additionally the server startup from a browser will always force a browser prompt of some sort, although if you opt to run the MM Web Server in always-on mode there will not be a prompt. It's best to start the server on demand even if that requires an extra operation if security is a concern.

### Using in a Web Page
The server can be accessed from client side code via a `markdownmonster-integration.js` file which provides a global `window.MarkdownMonster` object instance. This library has the following operations:

* **openNewDocument(newDocText)**  - opens a new document with the specified text
* **loadMarkdownMonster()** - uses an application protocol to explicitly launch Markdown Monster
* **checkServer(onCompleted)** - checks to see if the MM Web Server is running
* **openDocument(localDocFilename,onCompleted)** - opens a file in Markdown Monster
* **openNew(markdownText,onCompleted)** - opens a new document with optional text
* **getDocument(onCompleted)** - retrieves the content of the active editor window in Markdown Monster.
 
In most cases `openNewDocument()` is the only function required - it will check whether the server is running and if not prompt you and try to launch it.

The following example uses a text box with Markdown text and a button which when clicked opens the text in Markdown Monster:

```html
<textarea id="MarkdownText2"  ># Markdown text to edit</textarea>

<button id="btnOpenInMarkdownMonster2" class="btn btn-primary mt-2" onclick="openInMmWithWebServer()">
<img src="images/MarkdownMonster_Icon_32.png" style="height: 20px;margin-right: 10px" />
Open in Markdown Monster</button>

<!-- support library that can call the Web server (in `/SampleDocuments/BrowserIntegration/`) -->
<script src="markdownmonster-integration.js"></script>

<script>
    // initialize object during page load
    var mm = window.MarkdownMonster;            // global instance
    //mm.serverUrl = "http://localhost:15000"     // if you changed the port in mm :5009 is default
    mm.initialize();                            // checks for server
    function openInMmWithWebServer() {
        var text = document.getElementById("MarkdownText2").value;        
        
        // if server is running opens a new doc in Markdown Monster
        // if server is not running prompts to run MM and open in Web Server mode
        mm.openNewDocument(text);               
    }
</script>
```

You can find an example you can run in the `<installFolder>\SampleDocuments\BrowserIntegration` folder.

### Message Format
The messages sent to the server are `POST` operations using a JSON request pay load. For now this is very simple and abstracted by the JavaScript `markdownmonster-integration.js` script library.

To access the server assuming it's running:

* Make an HTTP POST request to `http://localhost:5009/`
* JSON: `{ operation: "open", data: "untitled.base64,VGhpcyBpcyBhIHRlc3Qgc3RyaW5nIG9mIHRleHQu" }`

This opens a new document with the base64 text content preset in the editor. This works with any of the single command [command line options](VFPS://Topic/_5FP0XP68P) in MM. 

* Open a new blank document
* Open new document with pre-set text
* You can open a file from a file system path


### Http Request Traces
Following are examples of HTTP request traces that can be used to interact with Markdown Monster.

```http
POST http://localhost:5009/markdownmonster HTTP/1.1
Content-Type: application/json

{
  "Operation": "open",
  "Data": "untitled.json,'# New Document\n\n\"This\" is a test **document**!'",
  "Type": "text",
  "Activate": true
}

------------------------------------------------------------------

POST http://localhost:5009/markdownmonster HTTP/1.1
Content-Type: application/json

{
  "Operation": "openNew",
  "Data": "# New Document\n\n\"This\" is a test **document**!",
  "Type": "text",
  "Activate": true
}

------------------------------------------------------------------

POST http://localhost:5009/markdownmonster HTTP/1.1
Content-Type: application/json

{
  "Operation": "openDocument",
  "Data": "c:\\temp\\test.md",
  "Type": "text",
  "Activate": true
}

------------------------------------------------------------------

POST http://localhost:5009/markdownmonster HTTP/1.1
Content-Type: application/json

{
   Operation: "getDocument",
   Data: null,
   Type: "json"
}
```

Remember in order for these operations to work the server has to be running.

### Web Server Configuration
The Web Server can be configured with 3 values in the configuration settings:

```json
{
  "WebServer": {
    "Port": 5009,
    "AutoStart": false
  },
}
```

> Additionally there's an internal `IsRunning` property which **is not persisted** over shutdowns. This setting controls the manual toggle on the **Tools->Web Server** menu. Unless you have `AutoStart=true` this setting is not persisted over Markdown Monster restarts, so to always run Web Server you need to set `AutoStart=true`.