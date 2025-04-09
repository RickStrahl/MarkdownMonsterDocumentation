Markdown Monster allows you to create custom Markdown Parsers that can be plugged into the Markdown Editor and that show up in a drop down on the statusbar:

![](/images/CustomMarkdownParsers.png)

We've provided a [PanDoc Add-in](https://github.com/RickStrahl/Pandoc-MarkdownMonster-Addin) that you can check out to see how to add a custom Markdown parser for Markdown Monster.

Custom markdown editors are useful for specialized tasks that the default parser doesn't do, or even if you want to extend the behavior of the default <a href="https://github.com/lunet-io/markdig" target="top">MarkDig parser</a> with additional functionality.

> #### @icon-info-circle Markdig Extension Preferred
> Markdown Monster uses the <a href="https://github.com/lunet-io/markdig" target="top">Markdig parser</a> and it's the preferred parser to use as it also provides features used in preview rendering. You can extend Markdig via Markdig Pipeline extensions, or extend via code in a Markdown Monster addin using string/RegEx manipulation of the input markdown or html output.

### Creating a Custom Markdown Parser Addin
Custom parsers are created as an **Addin** that simply override the `GetMarkdownParser()` method and provide an `IMarkdownParser` interface.

The easiest way to is to use <a href="https://marketplace.visualstudio.com/items?itemname=rickstrahl.markdownmonsteraddinproject" target="top">Visual Studio Markdown Monster Addin Project Template</a> to create a new Addin.

Here are the steps:

* Create a new Markdown Monster Addin Project
* Name the project CustomMarkdownParser**Addin**
* In generated class change the `Id` and `Name` properties  
  in `OnApplicationInitialized()` (remove the rest)
* Override the `GetMarkdownParser()` method
* Implement your parser and return it in that method

### The Addin Class: Implement GetMarkdownParser()
The addin class for a custom parser addin is simple:

```csharp
public class CustomMarkdownParserAddin : MarkdownMonster.AddIns.MarkdownMonsterAddin
{
    public override Task OnApplicationInitialized(AppModel model)
    {
        // Remove 'Addin' from the Id
        Id = "CustomMarkdownParser";
        Name = "Custom Markdown Parser";            
        
        return Task.CompletedTask;
    }

    public override IMarkdownParser GetMarkdownParser(bool usePragmaLines, bool force)
    {
        return new CustomMarkdownParser();
    }
}    
```

This mostly involves removing code from `OnApplicationInitialized()` and implementing `GetMarkdownParser(bool usePragmaLines, bool force)`.

### Creating a custom Markdown Parser Class
Creating a new markdown parser is also easy: Simply implement the `IMarkdownParser` interface which merely consists of the `Parse(markdown)` method. You can inherit from `MarkdownParserBase` to get some base functionality but that is optional.

```csharp
public class PandocMarkdownParser : IMarkdownParser
{
        public override string Parse(string markdown) 
        {
            string html;
            
            // do your markdown conversion logic
            
            return html;
        }
}
```

You can create your own from scratch or you can subclass from either `MarkdownParserBase` (which includes some markup features), or the `MarkdownParserMarkdig` which is the default parser Markdown Monster uses based on Markdig. This is useful if you want to add custom functionality ontop of existing functionality such as special markup that can be injected before or after the markdown parsing occurs.

```csharp
public class CustomMarkdownParser : MarkdownParserMarkdig
{
    public CustomMarkdownParser(bool pragmaLines = false, bool forceLoad = false) 
                        : base(pragmaLines, forceLoad)
    { }
        
    public override string Parse(string markdown)
    {
        // inject some additional text
        return "&copy; Custom Markdown Inc<hr />" + 
        base.Parse(markdown);
    }
}
```

And that's it!

Compile the project and make sure it goes into its own folder in (if you used the template this should be set by default):

```txt
%appdata%\Markdown Monster\Addins
```

and that the addin `.dll` ends in **Addin.dll** (ie. MyCustomMarkdownParser**Addin**.dll). 

### Switching parsers in Markdown Monster
The parser dropdown on the status bar only shows up if there are custom parsers registered. If there are you can use the dropdown to select your parser, which should immediately re-render the current document with the new parser.

### Scroll Syncing Considerations
Markdown Monster's preview window relies on line information in the generated HTML to sync the editor location and preview. This takes the form of `pragma-line-x` Ids being generated into the parser when previewing:

```html
<h1 id="pragma-line-2">Markdown Monster Change Log</h1>
<p id="pragma-line-3"><small>
  <a href="https://markdownmonster.west-wind.com/download.aspx">download latest version</a> • 
  <a href="https://chocolatey.org/packages/MarkdownMonster">install from Chocolatey</a> • 
  <a href="https://markdownmonster.west-wind.com">Web Site</a></small>
</p>
<h3 id="pragma-line-6">1.8.15</h3>
<p id="pragma-line-7"><em><small>not released yet</small></em></p>
```

Markdown Monster uses the excellent <a href="https://github.com/lunet-io/markdig" target="top">Markdig</a> parser for creating markdown and it includes a **pragma-lines** option. If you use another Markdown Parser it may or may not support this functionality and **if it doesn't preview syncing will not work**.

If possible we'd recommend overriding the Markdig parser either via a Markdig extension or by extending the custom MarkdownParser functionality (most likely via string and RegEx manipulation of the generated output) inside of your C# addin code.