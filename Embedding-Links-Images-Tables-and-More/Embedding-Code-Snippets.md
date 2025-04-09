You can easily embed code snippets into your Markdown Text:

* Indented Markdown Code
* Github Flavored Code Snippets
* [Paste Code Dialog for quick Code Pasting](#ThePasteCodeDialog)

## Indented Code Blocks
Markdown considers any text indented with 4 or more spaces, or a tab as a **code block**.

So, this markdown (with 4 leading spaces or a tab):

```markdown
    var config = new WeblogConfiguration();
    // load configuration settings
    Configuration.Bind("Weblog", config);   
    services.AddSingleton(config);
```

renders into a code block like this:

    var config = new WeblogConfiguration();
    // load configuration settings
    Configuration.Bind("Weblog", config);   
    services.AddSingleton(config);
    
Indented code blocks try to identify syntax based on auto-discovery - here the language is assumed to be a c-style language (c# in this case), but this may not always be 100% accurate.

> #### Preview and Live Site Code Rendering Differences
> The behavior of the preview (MM uses [highlightJS](https://highlightjs.org/)) may differ than what you may see on a target site such as GitHub as different syntax highlighting tools are used. Especially auto-detection may vary significantly which is why we recommend you use **GitHub flavored Code Blocks**.

## GitHub Flavored Code Blocks
GitHub flavored code blocks are more explicit about the code representation by not relying on leading spacing but rather using a triple back tick plus a syntax language code delimiter at the beginning and triple backslashes at the end of a code block.

Using this approach, the following HTML syntax block in Markdown:

![](/images/markdowncode.png)

renders as a code block like this:

```html
<div class="product-image-wrapper">
    <img class="product-image"
         src="markdownmonster.png" />
</div>
```

You can specify a slew of languages, mostly by their file extensions:

```
cs,ts,js,html,css,md,xml,php,py,prg,cpp,bat,ini
```

and many more. Many formats also have longer names (like `csharp,javascript,powershell` etc.) that can be used. For recommended values you can use the **Paste Code Dialog** to paste your code.

## The Paste Code Dialog
Although entering code manually using Markdown text is easy, it can be time consuming as you have to paste the code, add the delimiters and then also left align the code. You can also use the **Paste Code Dialog** and save quite a few keystrokes in the process. 

> The dialog picks up code from a **selection in the editor** or the **clipboard** and it automatically **strips leading whitespace** from your code blocks.

You can access the Paste Code dialog by pressing `alt-c` or clicking the code icon on the **{#}** toolbar icon:

![](/images/pastecodesnippet.png)

> The Code Language dropdown remembers the last language you used

You can edit the code in the code edit box and select a language from the language drop down. The drop down auto-completes, so typing a letter or two of the language usually selects it.

This can make for a **very quick code pasting workflow**:

* Select code in another editor or textbox and copy to clipboard
* Go to Markdown Monster
* Press `alt-c` in the editor
* Type a letter or two for syntax type (ie. html)
* Press `Enter`

The code block text is pasted at the current cursor position!