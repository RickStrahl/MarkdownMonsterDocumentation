You can create new sidebar tabs which effectively allows you to display custom content that is more complex but needs to stay open while the editor is running. Examples of sidebars including the Folder Browser, Document Outline, or the KavaDocs Documentation content tree.

### Creating a Sidebar Panel
The code to add a new sidebar panel is as follows:

```csharp
// Set up the KavaDocs Topic Tree in the Left Sidebar
var tabItem = new MetroTabItem() {Name = "KavaDocsTree"};

// Create the tab content user control
KavaDocsTopicTreeTab = tabItem;
Tree = new TopicsTree();
tabItem.Content = Tree;

// Create an ImageSource for the icon (custom code here)
var icons = new AssociatedIcons();
var imgSource = icons.GetIconFromFile("t.kavadocs");  // image source

Model.Window.AddLeftSidebarPanelTabItem(tabItem,"Kava Docs",imgSource);
```

Note that it's not necessary to create an image icon - you can just provide text but we recommend that you do provide an icon. The icon will be resized to 16x16.

### Create a standard Toolbar Header
A sidebar panel should typically have a side bar header that includes an icon and name on the left and one or more icons. The right most icon should be a closing chevron to close the sidebar.

The following is the top grid row for a typical sidebar layout:

```xml
<Grid Background="{StaticResource SidebarHeaderBackground}">
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="*" />
        <ColumnDefinition Width="Auto" />
    </Grid.ColumnDefinitions>

    <StackPanel Orientation="Horizontal">
        <fa:FontAwesome Icon="Bookmark" Foreground="Goldenrod" Height="16" Width="16" Margin="5,2,0,0" />
        <TextBlock Height="Auto" 
                   Text="Favorites"  
                   FontWeight="SemiBold" FontSize="11"  Padding="4,5,2,5" />
    </StackPanel>

    <Button  fa:Awesome.Content="ChevronCircleLeft" Background="Transparent" 
             Foreground="{DynamicResource BlueItem}" Padding="7,0,7,0" Grid.Column="1"  
             Name="ButtonClosePanel" BorderThickness="0" FontSize="12"                     
             ToolTip="Close Sidebar Panel" 
             Command="{Binding AppModel.Commands.CloseLeftSidebarPanelCommand}" />
</Grid>
```

which looks like this:

![](//images/sidebarheader.png)