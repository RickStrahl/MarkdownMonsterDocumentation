There are a few different ways you can specify icons for to be displayed on the toolbar for your addin. Addin icons are sequentially added to the end of the rightmost toolbar.

![](//images/AddinsToolbar.png)

You'll notice that the icons on the toolbar have varying icons. The first three icons are image icons, while the last two are FontAwesome icons.

### Specifying Icons in the Addin
The basic process of adding icons is done as part of the `OnApplicationInitialized()` operation:

The following uses a FontAwesomeIcon and optional color:

```cs
public override Task OnApplicationInitialized()
{
    Id = "PasteCodeAsGist";

    AddinMenuItem = new AddInMenuItem(this)
    {
        Caption = "Gist",
        FontawesomeIcon = FontAwesomeIcon.Github,
        FontawesomeIconColor = "#247CAC"
    };

    MenuItems.Add(AddinMenuItem);            
    
    return Task.CompletedTask;
}
```

Alternately you can also specify an `ImageSource`. Instead of the `Fontawesome`  properties set the `IconImageSource` property instead:

```cs
AddinMenuItem = new AddInMenuItem(this)
{
    Caption = "Gist",
    FontawesomeIcon = FontAwesomeIcon.Github,
    FontawesomeIconColor = "#247CAC"
}

try 
{
  AddinMenuItem.IconImageSource = new ImageSourceConverter()
        .ConvertFromString("pack://application:,,,/GistIntegrationAddin;component/icon_22.png") 
        as ImageSource
}
catch{ }
```

> ### @icon-info-circle Image Resources
> We recommend when you use image resources that you also specify a FontAwesome icon and put the image retrieval into a `try/catch` block. Should the image retrieval fail, your addin will still load with the FontAwesome icon as a fall back.

> ### @icon-info-circle Threading Issue
> Markdown Monster performs initial addin loading asynchronously on a separate thread, so when the icons are initially attached, you may not be on the UI thread. This can in some cases cause odd behavior with WPF when loading images from external resources. If you run into trouble with this, see the section on post-processing images in the `OnWindowLoaded()` event.

### Modifying the Menu Button and Image Icon
The above options allow you to assign either a font-awesome icon or a simple image resource. If you need to perform additional modification on either the icon or the menu item itself you can do this in the `OnWindowLoaded()` event which provides access to the Menu Button via the `Addin.MenuItemButton` property.

The following example completely replaces the existing icon with a new icon image source and explicitly manipulates the menu button size:

```cs
public override void OnWindowLoaded()
{
    var mButtonContent = AddinMenuItem.MenuItemButton?.Content;
    if (mButtonContent != null)
    {
        var image = (Image) mButtonContent;
        image.Source = ImageAwesome.CreateImageSource(FontAwesomeIcon.GithubAlt, new BrushConverter().ConvertFrom("#247CAC") as Brush);
        image.Height = 22;
        image.Width = 22;
    }
```

### Not Showing Addin Buttons And DropDowns
In some cases you may have addins that don't need to show an Icon or menu item, or only needs to show the main icon  but not a configuration option. You can control these UI items by disabling their respective execution handlers, which by default point at the addins `OnExecute` and `OnExecuteConfiguration` methods. By setting them to null you disable their functionality and their UI.

To remove the Toolbar Icon altogether, simply set the `Execute` Task to `null`:

```csharp
var menuItem = new AddInMenuItem(this)
{
	Caption = "Non Visible Addin",
	Execute = null
};
MenuItems.Add(menuItem);
```

An example of a non-visible Markdown Monster Addin may be a custom Markdown parser addin that only replaces the parser transparently.

To remove the Configuration drop down but leave the main icon in place:

```csharp
var menuItem = new AddInMenuItem(this)
{
	Caption = "No Config Addin",
	ExecuteConfigration = null
};
MenuItems.Add(menuItem);
```

An example of an addin that doesn't have configuration is the Chromium WebView Previewer addin which only uses the main Toolbar button as an on-off toggle and has no additional configuration.