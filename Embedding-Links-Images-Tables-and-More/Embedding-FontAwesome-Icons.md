Markdown Monster can easily embed FontAwesome icons into your Markdown text. If your target site's styles load FontAwesome you can take advantage of MM's simplified FontAwesome embedding.

To add a FontAwesome Icon simply use the **&#64; icon-iconName** shortcut to embed the icon. For example, the following adds FontAwesome's round circle info icon into the text below:

> #### @icon-warning-color:darkgoldenrod Markdown Monster Specific Feature
> This format is a **custom extension** that is not supported outside of Markdown Monster, or tools that use its markdown engine. You can generate HTML and PDF output from MM or publish HTML to a Weblog from this output, but it will not render by default in hosted services like GitHub. A [custom code implementation](#fontawesome-extension-parsing-implementation-code) along with a .NET based Markdown parser that includes this RenderExtension, for handling the conversion is provided below.




```markdown
> #### @ icon-info-circle Notice
> blah blah blah
```

which produces:

> #### @icon-info-circle Notice
> blah blah blah

Notice the icon info icon which is embedded by the **&#64; icon-info-circle** syntax, which is responsible for the embedded icon. 

Here's another example:

```markdown
Click on the @ icon-camera icon to take a screen shot.
```

which produces:

<div class='well'>
Click on the @icon-camera icon to take a screen shot.
</div>

To insert a FontAwesome Icon, simple use **&#64; icon-** followed by the <a href="http://fontawesome.io/icons/http://fontawesome.io/icons/" target="top">FontAwesome Icon name</a> which you can find on the FontAwesome web site.
 
All of Markdown Monster's Preview styles include FontAwesome styles so the preview and exported documents will always include the FontAwesome icons.

### More sophisticated Icon Usage via HTML
You can also use more sophisticated icon displays, like rotations for example, but for those you have to use HTML markup:

```markdown
> #### <i class="fa fa-gear fa-spin fa-2x" style="color: firebrick"></i> Configuration
> Configuration can be launched from the **Tools -> Settings** menu option.
```

which produces: 

> #### <i class="fa fa-gear fa-spin fa-2x" style="color: firebrick"></i> Configuration
> Configuration can be launched from the **Tools -> Settings** menu option.

Icons are a great way for callouts or quote blocks, as they can make content more visually interesting. But don't overuse these icons and use them consistently on your sites and documentation.

> #### @icon-warning Requires FontAwesome on your Site
> It's important to understand that FontAwesome Icons only work if FontAwesome is loaded into the HTML page. Markdown Monster's preview themes all include FontAwesome on the preview page, but your target Web site or documentation may not include it, in which case the icons will not render. 
>
> Make sure that FontAwesome is available on your output target before using this feature.

## Font Customizations
There are several additional FontAwesome Style Extensions that you can apply to your embeddings via `-` directives.

* Font styles (`@ icon-solid`, `@ icon-duotone`, `@ icon-light`, `@ icon-regular`)
* Font color (`-color:gold`)
* Spinning icons (`-spin`)

Example:

```markdown
@ icon-duotone-spinner-spin-color:steelblue Spin me up!
```

> @icon-duotone-spinner-spin-color:steelblue Spin me up! {style="font-size: 2em"}

## IMPORTANT: Custom Extension!
These features are a  custom Render Extension that Markdown Monster provides and that are **not supported** by most hosting services. 

It works for:

* Markdown Monster Preview
* Markdown Monster HTML output
* Markdown Monster PDF Output
* [Westwind.AspnetCore.Markdown](https://github.com/RickStrahl/Westwind.AspNetCore.Markdown) rendering (.NET)

### FontAwesome Extension Parsing Implementation Code
The rendering format is implemented as follows and can be easily implemented as a Markdown pre-processor as demonstrated by the RenderExtension implementation that takes the Markdown text as input (in `args.Markdown` in the sample code):

```cs
public class FontAwesomeRenderExtension : IMarkdownRenderExtension
{
    public string Name { get; set; } = "FontAwesomeRenderExtension";

    static Regex fontAwesomeIconRegEx = new Regex(@"@icon-.*?[\s|\.|\,|\<]");

    public void BeforeMarkdownRendered(ModifyMarkdownArguments args)
    {
        var md = args.Markdown;

        var matches = fontAwesomeIconRegEx.Matches(md);
        foreach (Match match in matches)
        {
            string iconblock = match.Value.Substring(0, match.Value.Length - 1);

            string faPrefix = "fas";
            string icon = null;
            if (iconblock.StartsWith("@icon-regular-"))
            {
                faPrefix = "far";
                icon = iconblock.Replace("@icon-regular-", "");
            }
            else if (iconblock.StartsWith("@icon-duotone-"))
            {
                faPrefix = "fad";
                icon = iconblock.Replace("@icon-duotone-", "");
            }
            else if (iconblock.StartsWith("@icon-solid-"))
            {
                faPrefix = "fas";
                icon = iconblock.Replace("@icon-solid-", "");
            }
            else if (iconblock.StartsWith("@icon-light-"))
            {
                faPrefix = "fal";
                icon = iconblock.Replace("@icon-light-", "");
            }
            else
            {
                faPrefix = "fas";
                icon = iconblock.Replace("@icon-", "");
            }


            string color = null;         
            var idx = icon.IndexOf("-color:");
            if (idx > 0)
            {
                var extr = Westwind.Utilities.StringUtils.ExtractString(icon, "-color:", "-", caseSensitive: false, allowMissingEndDelimiter: true, returnDelimiters: true);
                color = Westwind.Utilities.StringUtils.ExtractString(extr, "-color:", "-", caseSensitive: false, allowMissingEndDelimiter: true, returnDelimiters: false);
                if (!string.IsNullOrEmpty(color))
                {
                    color = $";color: {color}";
                    icon = icon.Replace(extr.TrimEnd('-'), string.Empty);
                }
            }


            if (iconblock.EndsWith("-spin") || iconblock.Contains("-spin-"))
                icon = icon.Replace("-spin", " fa-spin ");

            md = md.Replace(iconblock, $"<i class=\"{faPrefix} fa-" + icon + $"\" style=\"font-size: 1.1em{color}\"></i> ");
        }

        if (md != args.Markdown)
            args.Markdown = md;
    }

    public void AfterMarkdownRendered(ModifyHtmlAndHeadersArguments args)
    { }

    public void AfterDocumentRendered(ModifyHtmlArguments args)
    { }

}
```