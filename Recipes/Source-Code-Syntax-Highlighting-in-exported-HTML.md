Markdown by design doesn't create HTML with embedded source code formatting, as it generates just a block of HTML. Unless you exported HTML with all assests that you see in the preview, the output doesn't automatically show syntax coloring.

### Markdown Code Output
Markdown dictates that code blocks are exported as plain `<pre><code>` blocks into HTML, and it's up to the hosting page or application to provide the syntax highlighting.

MM's previewer includes the logic via JavaScript to render the code blocks as highlighted HTML using the <a href="https://highlightjs.org/" target="top">highlightJS</a> Javascript library.

For example a block of HTML code that is highlighted like this:

```html
<nav class="nav-header">
    <a href="#home" class="nav-button">Home</a>
    <a href="#article" class="nav-button">Articles</a>
</nav>
```

is actually rendered in the underlying HTML like this:

```html
<pre><code class="language-html">&lt;nav class=&quot;nav-header&quot;&gt;
    &lt;a href=&quot;#home&quot; class=&quot;nav-button&quot;&gt;Home&lt;/a&gt;
    &lt;a href=&quot;#article&quot; class=&quot;nav-button&quot;&gt;Articles&lt;/a&gt;
&lt;/nav&gt;
</code></pre>
```

HighlightJS then turn this HTML into nicely syntax colored text you see in the first code sample. There are a number of other JavaScript based Syntax Highlighters available, but highlightJs is amongst the easiest and fastest rendering ones so that's what we provide.

Note that code is HTML encoded so it's safe to display without script injection, but the actual code is not in any way marked up for syntax coloring other than using the start tags that identitify the optional syntax in use:

```html
<pre><code class="language-html">
<!--...code here...-->
</code></pre>
```

### Example using HighlightJs 
Markdown Monster uses <a href="https://highlightjs.org/" target="top">HighlighJs</a> for syntax highlighting in the previewer and for full HTML exports, and you can see how the default highlighting works in the HTML Preview Pane of Markdown Monster's UI. HighlightJs is open source and you can easily add HighlightJs on your Web site with just a script and css reference, plus couple of lines of JavaScript code.

> #### @icon-info-circle Other Highlighters
> You can use any kind of JavaScript based highlighter. For example, MM originally used AceEditor for highlighting. The integration syntax might be slightly different, but the process is usually quite easy to set up similar to what we show here for HighlightJs.

To integrate HighlightJS into your own Website or Weblog:

* Add the highlightJS JavaScript and CSS Styles to your page
* Add a small snippet of script code into your HTML page

#### HighlightJs Example
In order to use HighlightJs you can copy the following folder:

**<MM Install Folder>PreviewThemes\scripts\highlightjs**

You can add the following to your HTML document to enable syntax coloring:

```html
<link href="scripts/highlightjs/styles/github-gist.css" rel="stylesheet" />
<script src="scripts/highlightjs/highlight.pack.js"></script>

<!--<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.11.0/styles/default.min.css">-->
<!--<script src="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.11.0/highlight.min.js"></script>-->

<script>
function highlightCode() {
    var pres = document.querySelectorAll("pre>code");
    for (var i = 0; i < pres.length; i++) {
        hljs.highlightBlock(pres[i]);
    }
}
highlightCode();
</script>

</body>
</html>
```

The first CSS style-sheet is the code style - in this case `github-gist`. Choose from any of the other styles available in the `styles` folder.

Note that you can also use the online CDN link that commented out in the code above:

```html
<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.11.0/styles/default.min.css">
<script src="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.11.0/highlight.min.js"></script>
```

### Syntax Style Themes
The stylesheet link determines the code highlight theme above it's **github-gist**. You can choose from others defined in the `highlightjs/styles` folder. 

Some other popular ones:

##### Dark Themes
* vs2015   (Visual Studio Dark or VSCode Dark)
* twilight
* monokai
* monokai-sublime
* darkula

##### Light Themes
* vs  (Visual Studio)
* github
* github-gist
* textmate
* xcode

You can also copy and customize any of these themes to match your exact needs.


### Syntax Languages for Fenced Code Blocks
The following is a list of languages supported for fenced code blocks. You can use either of the formats shown.

#### Common Built In
* html
* xml
* css
* scss
* less
* js javascript
* cs csharp
* java

#### Custom
* typescript
* fsharp 
* vbnet vb
* foxpro prg 
* markdown md
* powershell ps
* batch bat
* dockerfile docker
* dos bat cmd
* swift
* objectivec
* dns
* txt none
* http
* yaml
* ini
* diff patch
* pgsql postgres
* python
* go
* rust