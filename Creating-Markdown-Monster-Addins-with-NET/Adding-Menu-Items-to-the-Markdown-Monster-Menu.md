You can also add new menu items to the existing Markdown Monster main menu by using the `AddMenuItem()` method on the Addin class.

To do this:

* Add an `OnWindowLoaded()` overload
* Create a Menu Item with Header and Click handler
* Call `Addin.AddMenuItem()`


`AddMenuItem()` allows adding a WPF menu item **before** or **after** and existing menu item, either by menuitem name or header text.


The following addin adds two menu items to Markdown Monster's *File* menu:

```cs
public override void OnWindowLoaded()
{
    // create and add custom menu item
    var mitemOpen = new MenuItem()
    {
        Header = "Open from Gist",
        Name = "ButtonOpenFromGist"
    };
    mitemOpen.Click += (s, a) => OnExecuteLoadGist();
    if (!AddMenuItem(mitemOpen, menuItemName: "ButtonOpenFromHtml", mode: 0))
        mmApp.Log("Unable to add custom menu item in Paste Code As Gist Addin: " + mitemOpen.Name);

    var mitemSave = new MenuItem()
    {
        Header = "Save to Gist",
        Name = "ButtonSaveToGist"
    };
    mitemSave.Click += (s, a) => OnExecuteSaveGist();
    if (!AddMenuItem(mitemSave, menuItemName: "ButtonGeneratePdf", mode: 0))
        mmApp.Log("Unable to add custom menu item in Paste Code As Gist Addin: " + mitemSave.Name);
}
```
> #### @icon-warning Use OnWindowLoad()
> Note that this code has to run in `OnWindowLoaded()` because it requires access to the Window and dispatcher. The default `OnApplicationStart()` doesn't have access to the Window and hence this requirement.

### AddMenuItem()
The AddMenuItem function lets you add a menu item before or after an existing menu item. To use it you provide a menu item, and either a menu item name or header caption. You can also specify whether the new menu item is added before or after the first match.

The signature is:

```cs
public bool AddMenuItem(MenuItem mitem, 
    string menuItemName = null, 
    string menuItemText = null, 
    int mode = 0)
```    

Mode is 0 for after and 1 before.

> #### @icon-info-circle Finding Menu Item Names
> You can check for Menu Item names in the Markdown Monster source code for <a href="https://github.com/RickStrahl/MarkdownMonster/blob/master/MarkdownMonster/MainWindow.xaml" target="top">MainWindow.xaml</a>.