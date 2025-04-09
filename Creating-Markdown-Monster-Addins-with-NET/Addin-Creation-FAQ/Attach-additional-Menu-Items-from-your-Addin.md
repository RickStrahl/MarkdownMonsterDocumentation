You can use the `OnWindowLoaded` method i to attach additional menu items to the menu. 

For example, the <a href="https://github.com/rickstrahl/gistintegration-markdownmonster-addin" target="top">Gist Integration Addin</a> adds two new menu items to - `Save as Gist` and `Open from Gist` - from to the default **File** menu using the following code:

```cs
// create and add custom menu item
var mitemOpen = new MenuItem()
{
    Header = "Open from Gist",
    Name = "ButtonOpenFromGist"
};
mitemOpen.Click += (s, a) => OnExecuteLoadGist();            
if (!AddMenuItem(mitemOpen, menuItemNameForInsertionAfter: "ButtonOpenFromHtml", mode: 0))
    mmApp.Log("Unable to add custom menu item in Paste Code As Gist Addin: " + mitemOpen.Name);

var mitemSave = new MenuItem()
{
    Header = "Save to Gist",
    Name = "ButtonSaveToGist"
};
mitemSave.Click += (s, a) => OnExecuteSaveGist();
if (!AddMenuItem(mitemSave, menuItemNameForInsertionAfter: "ButtonGeneratePdf", mode: 0))
    mmApp.Log("Unable to add custom menu item in Paste Code As Gist Addin: " + mitemSave.Name);
```

The key method is `AddMenuItem()` which allows you to specify the control name or caption of an existing menu item to insert a new menu item before (mode 1) or after (0). You can also replace existing menu items (2).