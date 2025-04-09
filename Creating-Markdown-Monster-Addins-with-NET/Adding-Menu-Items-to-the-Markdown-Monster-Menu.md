You can also add new menu items to the existing Markdown Monster main menu by using the `AddMenuItem()` method on the Addin class.

To do this:

* Add an `OnWindowLoaded()` overload
* Create a Menu Item with Header and Click handler
* Call `Addin.AddMenuItem()`


`AddMenuItem()` allows adding a WPF menu item **before** or **after** an existing menu item, either by menu item `Name` or the header text in the `Header` property. Important: The name or header have to match **exactly** in order for the existing menu item to be found. You can look up the [menu items in the source code](https://github.com/RickStrahl/MarkdownMonster/blob/master/MarkdownMonster/MainWindow.xaml#L224) - look for the `Name="MainMenu"` and look through the items there. 

> @icon-warning If the source menu item is not found the new menu item is not inserted and fails silently. The error is logged, but there's no visual clue that it failed in the UI.

By default new menu items are added after the matched element, but you can override and insert before or replace a menu item using the `addMode` enum parameter.

The following addin adds two menu items to Markdown Monster's *File* menu:

```cs
public override Task OnWindowLoaded()
{
    // create and add custom menu item
    var mitemOpen = new MenuItem()
    {
        Header = "Open from Gist",
        Name = "ButtonOpenFromGist"
    };
    mitemOpen.Click += (s, a) => OnExecuteLoadGist();
    if (!AddMenuItem(mitemOpen, menuItemNameForInsertionAfter: "ButtonOpenFromHtml"))
        mmApp.Log("Unable to add custom menu item in Paste Code As Gist Addin: " + mitemOpen.Name);

    var mitemSave = new MenuItem()
    {
        Header = "Save to Gist",
        Name = "ButtonSaveToGist"
    };
    mitemSave.Click += (s, a) => OnExecuteSaveGist();
    if (!AddMenuItem(mitemSave, menuItemNameForInsertionAfter: "ButtonGeneratePdf"))
        mmApp.Log("Unable to add custom menu item in Paste Code As Gist Addin: " + mitemSave.Name);
        
    return Task.CompletedTask;
}
```
> #### @icon-warning Use OnWindowLoad()
> Note that this code has to run in `OnWindowLoaded()` because it requires access to the Window and dispatcher and that the window and controls are already loaded. `OnWindowInitialized()` fires too early for direct UI interactions.

### AddMenuItem()
The AddMenuItem function lets you add a menu item before or after an existing menu item. To use it you provide a menu item, and either a menu item name or header caption. You can also specify whether the new menu item is added before or after the first match.

The signature is:

```cs
public bool AddMenuItem(
  MenuItem mitem,
  string menuItemNameForInsertionAfter = null,
  string menuItemTextForInsertionAfter = null,
  AddMenuItemModes addMode = AddMenuItemModes.AddAfter)
```    

> #### @icon-info-circle Finding Menu Item Names
> You can check for Menu Item names for use in `menuItemNameForInsertionAfter` in the Markdown Monster <a href="https://github.com/RickStrahl/MarkdownMonster/blob/master/MarkdownMonster/MainWindow.xaml" target="top">MainWindow.xaml source code</a>. Note that not all menu items have names, so for those that don't use can use the menu item's `Header` property or content value instead with  `menuItemTextForInsertionAfter`.