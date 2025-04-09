Markdown Monster supports intercepting the Markdown and generated HTML and making modifications using full featured .NET Addins or - for simple things - using the <a href="https://github.com/RickStrahl/Commander-MarkdownMonster-Addin" target="top">Commander</a> or <a href="https://github.com/rickstrahl/snippets-markdownmonster-addin" target="top">Snippets</a> addins. Full addins take a bit of effort, but using the **Commander add in** can be very easy.

Here's a use case somebody asked about recently:

> I use HTML comments in my markdown to break up my Markdown text, but I don't want to render the comments into the output. Is there a way to strip the comments?

Yes it's possible to intercept the rendering process using a couple of events on the `MarkdownDocument` object in Markdown monster.

Using the Command add in you can create a commander script that looks like this:

![](/images/commandaddin-intercepthtml.png)

To do this:

* Use the Addin Manager to install the **Commander Addin**
* Use **Add Command** to create a new Command Script
* Enter the code shown below
* Run Command to test and make sure there are no compilation errors

To get the addin to work you need to run the command or you can create a hot key to activate it. **It will not automatically run** and the command is effectively bound to the document you run it on.

Here's the code that hooks up the event:

```cs
using System.Text.RegularExpressions

var doc = Model.ActiveDocument as MarkdownDocument;
doc.DocumentRendered += (html,markdown) =>
{
    if (string.IsNullOrEmpty(html))
        return html;
        
        
    return Regex.Replace(html, 
                 "<!--.*?-->", "",
                 RegexOptions.IgnoreCase | RegexOptions.Multiline);
};
```

### Creating an Addin
If you want a more permanent solution that fires without explicit interaction you can create a full addin.

* [Create Markdown Monster Addin](https://markdownmonster.west-wind.com/docs/_4ne0s0qoi.htm)
* [Creating non-visual Addins](https://markdownmonster.west-wind.com/docs/_4ut0j9cm6.htm)

    
Addins have a dedicated method for modifying the rendered HTML (or Markdown) `OnModifyPreviewHtml()` and you can override the HTML in this method using the same Regex logic used in the Commander script above. 

```cs
public class StripCommentsAddin : MarkdownMonster.AddIns.MarkdownMonsterAddin
{
    public override void OnApplicationStart()
    {
        Id = "StripCommentsAddin";
        Name = "Strip Comments From HTML";            
    }

    public override OnModifyPreviewHtml(html, markdown)
    {
        return Regex.Replace(html, 
                    "<!--.*?-->", "",
                    RegexOptions.IgnoreCase | RegexOptions.Multiline);
    }
}
```