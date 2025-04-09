When you create a Markdown Monster add-in you effectively have access to all of Markdown Monster's feature set. Not all the functionality is easily accessible, but a number of common features are surfaced on the **MarkdownMonsterAddin** base class that your Addin is inheriting from.

* Add-in Events
* Add-in Common Feature Methods

### LifeTime Events

* OnApplicationStart()
* OnApplicationInitialized()
* OnWindowLoaded()
* OnApplicationShutdown()

### Installation Events
* OnInstalled()
* OnUninstalled()

### Document Related Events
In addition to the main Execute events, the add-in exposes a number of document related events that you can intercept as well:

* OnBeforeOpenDocument()
* OnAfterOpenDocument()
* OnBeforeSaveDocument()
* OnAfterSaveDocument()
* OnSaveImage()
* OnNotifyAddin()
* OnEditorCommand()
* OnDocumentActivated()

### Previewer Handling

* OnModifyPreviewHtml()
* OnPreviewLinkNavigation()

You can override these events to hook the specific operations you are interested in.

For example if you want to add custom logic when a document is saved you can do something like this:

```csharp
public override bool OnBeforeSaveDocument(MarkdownDocument doc)
{
    string file = doc.Filename;
    string text = doc.CurrentText;
    bool isValid = true;
    
    
    // ...
    // do something with the document
    // You can use 'Model' to access Window, Configuration, Editor etc.
    // ...
    
    return isValid;
}
```
You can simply override the relevant methods and look at the active document.