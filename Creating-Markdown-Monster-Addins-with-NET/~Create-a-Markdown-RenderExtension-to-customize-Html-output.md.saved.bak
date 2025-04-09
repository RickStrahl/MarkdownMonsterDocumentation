RenderExtensions in Markdown Monster allow you to customize the HTML output that is created as part of the rendering pipeline by pre or post processing the generated markdown or html content.

You can do this implementing the `IMarkdownRenderExtension` interface, and adding the resulting RenderExtension to `RenderExtensionsManager.Current.RenderExtensions`.

This is a tree step process:

* Create a new Markdown Monster Addin
* Override only the `OnApplicationStart()` method
* Create your `IMarkdownRenderExtension` derived class implementation
* Add your extension to the Extension Manager

## The IMarkdownRenderExtension Interface
Render Extensions work by providing pre- and post-rendering hook methods that allow you inspect and modify the incoming markdown and outgoing HTML content and are implemented via a simple `IMarkdownRenderExtesion` interface.

The `IMarkdownRenderExtension` interface is defined as follows ([github](https://github.com/RickStrahl/MarkdownMonster/blob/master/MarkdownMonster/RenderExtensions/IMarkdownRenderExtension.cs)):


```csharp
/// <summary>
/// Interface implemented for RenderExtensions that allow modification
/// of the inbound Markdown before rendering or outbound HTML after
/// rendering as well as any custom code that needs to be injected
/// into the document header prior to rendering.
///
/// Use the `RenderExtensionsManager.Current.RenderExtensions.Add()` to
/// add any custom extensions you create.
/// </summary>
public interface IMarkdownRenderExtension
{
    void BeforeMarkdownRendered(ModifyMarkdownArguments args);
    void AfterMarkdownRendered(ModifyHtmlAndHeadersArguments args);
    void AfterDocumentRendered(ModifyHtmlArguments args);
}
```

### Interface Members
The interface provides 3 different hooks:

* **BeforeMarkdownRendered**   
Fired just before markdown is rendered into HTML. You can look at and modify the Markdown text and thus affect the render process. You also get passed the document for additional information and you have of course access to the model.   
*You can change: `args.Markdown`*

* **AfterMarkdownRendered**  
Occurs just after the Markdown text has been rendered into an **HTML Fragment** of just the Markdown content. The result HTML is in `args.Html` and it's just the raw HTML fragment where the Preview template has not been applied yet: This means there's no `<html>` or `<body>` or `<head>` but only the body content fragment. 

You can modify `args.Html` to affect rendering of the HTML. Additionally you can also set `args.HeadersToEmbed` to apply headers that are rendered into the bottom of the `<head>` section of the template when the template is rendered later in the pipeline. If you can modify HTML from the rendered Markdown, it's better to do it here, than in `AfterDocumentRendered` because this HTML is always refreshed.  
*You can change: `args.Html` and `args.HeadersToEmbed`*

* **AfterDocumentRendered**  
Occurs after the final HTML document has been rendered and merged with the Preview template. This is essentially the final HTML output before output is written to disk or to string for previewing as HTML. This is specific to full page output that is rendered in the preview, as well as used for PDF or HTML output generation.
*You can change: `args.Html`*

The `args` parameter passed contains the input and output data and the updatability of the properties for each of those parameter values depends on the property's `readwrite` or `readonly` status. 

## Create an Addin and Hook up a Render Extension in `OnApplicationStart()`
In order to add a Render Extension you need to be hooked into Markdown Monster's processing pipeline and so you need to create a [Markdown Monster addin](VFPS://Topic/_4NE0S0QOI). The addin is going to be very simple and needs to implements only the `OnApplicationStart()` method since the addin is non-visual. Use `OnApplicationStart()` as it also allows render extensions to be fired in the MM CLI.

In `OnApplicationStart()` you can then hook up the Render Extension for addition into the processing pipeline.

Here's the entire Addin class code:

```csharp
public class TestRenderExtensionAddin : MarkdownMonster.AddIns.MarkdownMonsterAddin
{
    public TestRenderExtensionAddin() : base()
    {
        Id = "TestRenderExtension";    
    }

    public override async Task OnApplicationStart()
    {
        await base.OnApplicationStart();
        
        // Add the render extension
        MarkdownRenderExtensionsManager.Current.AddRenderExtension(new TestRenderExtension());
    }
}
```

Yup - it's real small, because a render extension is non-visual, so you can remove all other generated addin code and keep just this minimal `OnApplicationStart()` logic which helps minimize the impact of this addin.

## Implementing a MarkdownRenderExtension
Let's create a super simple and frivolous MarkdownRenderExtension that turns all occurrances of ` the ` in the text into a bold and upper case text using ` **THE** ` as the text replacement. And just for kicks lets also add a copyright notice to the bottom of the document which allows us to demonstrate both pre-processing the Markdown for the `THE` replacement and post-processing for the footer to add. 

> In theory both of these transformations could be done in the same pre or post processing method - `BeforeMarkdownRendered()` being the preferred one for this scenarios since we're replacing actual Markdown text with other Markdown. I'm splitting up behavior here purely for demonstration purposes. 

To do this:

* Create a new `TestRenderExtension` class
* Assign a Name to identify the extension
* Inherit from `IMarkdownRenderExtension`
* Implement the interface - leave any unused methods empty but don't `throw`

```cs
public class TestRenderExtension : IMarkdownRenderExtension
{
    public string Name { get; set; } = "TestRenderExtension";

    public void BeforeMarkdownRendered(ModifyMarkdownArguments args)
    {
        var md = args.Markdown;
        md = md.Replace(" the "," **THE** ");
        args.Markdown = md;
    }

    public void AfterMarkdownRendered(ModifyHtmlAndHeadersArguments args)
    {
        args.Html += "<div class='alert alert-info'>&copy; Test Render Extension Company</div>";
    }

    public void AfterDocumentRendered(ModifyHtmlArguments args)
    { }
}
```

The result of this is that you get rendered HTML that has any individual words of the ` the ` show as bold, upper case **THE** text and a banner at the bottom of the page.

### A Note about Script Code: Refreshing Page Content in Script Code
If you inject script code into the page, realize that the script may have to be re-fired as content is refreshed. Markdown Monster doesn't re-render the entire page all the time, but rather replaces the content area with the rendered HTML content and if the script expects a page reload for updating content you need to notify or 're-run' the script code.

To allow script code to respond properly to this, there's an `previewUpdated` event that is fired when the document first loads and also when the preview is refreshed. So whatever initialization your script code needs, it's best to do this by handling this event.

```js
$(document).on('previewUpdated',function() {
    // do something with vueJs
    var v = new Vue('#MainContent');

    // silly stuff...
    setTimeout(function() { $('pre>code').css('background','darkgreen');  },3000);
});
```            

## A more practical example
Here's a more practical example that's provided as part of Markdown Monster which is the Mermaid charting addin. Mermaid is a JavaScript library that uses specific syntax embedded in HTML to render a host of relationship charts.

In order to render these MM needs to:

* Inject the Mermaid script from CDN
* Inject Mermaid initialization code
* Convert ` ```mermaid` into `<div class='mermaid'>`

Here's the code:

```cs
/// <summary>
/// Handles Mermaid charts based on one of two sytnax:
///
/// * Converts ```mermaid syntax into div syntax
/// * Adds the mermaid script from CDN
/// </summary>
public class MermaidRenderExtension : IMarkdownRenderExtension
{
    /// <summary>
    /// Add script block into the document
    /// </summary>
    /// <param name="args"></param>
    public void AfterMarkdownRendered(ModifyHtmlAndHeadersArguments args)
    {
        if (args.Markdown.Contains(" class=\"mermaid\"") || args.Markdown.Contains("\n```mermaid"))
            args.HeadersToEmbed = MermaidHeaderScript;
    }
    
    /// <summary>
    /// Check for ```markdown blocks and replace them with DIV blocks
    /// </summary>
    /// <param name="args"></param>
    public void BeforeMarkdownRendered(ModifyMarkdownArguments args)
    {
        while (true)
        {
            string extract = StringUtils.ExtractString(args.Markdown, "\n```mermaid", "```", returnDelimiters: true);
            if (string.IsNullOrEmpty(extract))
                break;

            string newExtract = extract.Replace("```mermaid", "<div class=\"mermaid\">")
                .Replace("```", "</div>");

            args.Markdown = args.Markdown.Replace(extract, newExtract);
        }
    }

    public void AfterDocumentRendered(ModifyHtmlArguments args)
    {     }



    private const string MermaidHeaderScript =
        @"<script src=""https://cdnjs.cloudflare.com/ajax/libs/mermaid/7.1.2/mermaid.min.js""></script>
<script>
mermaid.initialize({startOnLoad:false});
...
</script>";

}
```

If you need to build custom output generation functionality for Markdown Monster for creating custom syntax or simply intercepting HTML rendering output, RenderExtensions are an easy way to do this.

## Managing MarkdownRenderExtensions via the MarkdownExtensionManager
If for some reason you need to manage the existing Render Extensions you can use the various methods and accessors of the `MarkdownRenderExtensionsManager.Current` instance. 

* AddRenderExtension()
* RemoveRenderExtension()
* GetRenderExtensions()
* Retrieve a specific extension via the `[]` accessor

These helper allow you to check and avoid dual loading of addins for example or removing functionality that might interfere with your specific use case.