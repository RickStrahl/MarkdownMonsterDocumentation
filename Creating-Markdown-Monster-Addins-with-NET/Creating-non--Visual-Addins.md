Markdown Monster supports creating non-visual addins simply by not creating a menu item. In that case the addin simply fires addin events which you can hook into.

As with a regular addin you have to override `OnApplicationInitialized()` to initialize the add-in but you only set the `Id` and `Name` properties. Then go ahead and override any hook methods.

The following creates a custom, non-visual addin that intercepts document updates (ie. when the document value is actually captured when you stop typing), and frivolously writes out the generated HTML size into the status bar:

```csharp
public class CustomMarkdownAddin : MarkdownMonster.AddIns.MarkdownMonsterAddin
{
    public override Task OnApplicationInitialized(AppModel model)
    {
        Id = "CustomMarkdownParserAddin";
        Name = "Custom Markdown Parser";            
        
        return Task.CompletedTask;
    }

    // override one of the handled event hooks
    public override void OnDocumentUpdated()
    {
        var doc = Model.ActiveDocument;
        if (doc != null)
        {
            string html = doc.RenderHtml();
            Model.Window.ShowStatus("Rendered Html size: " + html.Length);
        }
    }
}
```