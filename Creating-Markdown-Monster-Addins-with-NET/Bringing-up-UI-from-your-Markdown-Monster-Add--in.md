Markdown Monster is a WPF application, so you can use WPF from within your Addin to bring up your own UI.

For example, the included <a href="https://github.com/rickstrahl/markdownmonster/blob/master/addins/weblogaddin/weblogaddin.cs" target="top">WebLog addin</a> brings up a relatively complex UI with code like this in the Addins `OnExecute()` overload:

```csharp
public override void OnExecute(object sender)
{
    
    var form = new WebLogForm()
    {
        Owner = Model.Window
    };
    form.Model.AppModel = Model;
    form.Model.Addin = this;                       
    form.Show();                       
}
```
Here's what the Addin looks like when it runs:

![](/images/WebLogAddIn.png)


### MahApps.Metro Forms
As you can see the Addin's form uses the same UI as the main application which is based on the awesome <a href="https://github.com/mahapps/mahapps.metro" target="top">MahApps.Metro library</a>. This is not required but if you build an addin for distribution it's probably a good idea to use the same UI styling.

To use a MetroWindow:

```xml
<controls:MetroWindow 
        x:Class="WeblogAddin.WebLogForm"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:MarkdownMonster;assembly=MarkdownMonster"
        xmlns:controls="http://metro.mahapps.com/winfx/xaml/controls"
        xmlns:fa="http://schemas.fontawesome.io/icons/"
        xmlns:dragablz="http://dragablz.net/winfx/xaml/dragablz"
        mc:Ignorable="d"        
        xmlns:weblog="clr-namespace:WeblogAddin"
        Title="Markdown Monster Weblog Addin" 
        TitleCaps="False"   
        WindowStyle="SingleBorderWindow" ResizeMode="CanResizeWithGrip"                      
        WindowStartupLocation="CenterOwner" 
        IsMinButtonEnabled="False" IsMaxRestoreButtonEnabled="False"                       
        Width="800" Height="625" MinHeight="650" MinWidth="600">

    <Grid>
       ...
    </Grid>
</controls>    
```

and in code make sure to inherit from `MetroWindow`:

```csharp
public partial class WebLogForm : MetroWindow
```

### Form to Markdown Monster Interaction
Once you have your form up and running you can easily interact with Markdown Monster using the `Addin` object or the `Addin.Model`, just as the other examples so far have done. You can grab editor selection, and update it with new content, open new tabs/documents or otherwise manipulate the UI.

If you want to see more of an advanced example on how to create a complex form based Addin take a look at the Weblog Addin which performs a number of different tasks that interact with Markdown Monster. For example, the Web log reads the entire Markdown document and adds a meta data footer to the bottom of the document. When posting to a Weblog that footer is stripped off and updated with the post id. It's possible to do pretty fine grained interaction between your form and Markdown Monster. The addin also allows for creation of a new post that creates a file and folder on disk and then opens the new document in a new tab in the editor.

For more info take a look at the source code here:

* <a href="https://github.com/RickStrahl/MarkdownMonster/tree/master/AddIns/WebLogAddin" target="top">Markdown Monster Weblog Publishing Addin</a>