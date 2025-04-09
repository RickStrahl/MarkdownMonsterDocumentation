The editor can be run in several different display modes:

* Normal mode 
* Distraction Free Mode
* Presentation Mode

These modes are primarily controlled via the Control Box at the top left of the Markdown Monster Window:

![](/images/EditorModesControlBox.png)

### Normal Mode
This is the default configuration which shows the editor with all the toolbars status bars and previewer. This is the most common way most people use the application.

### Toggle the Preview Window
Within the normal mode you can also toggle the previewer using the **@icon-globe World icon** on the Window control box, or using the **alt-v-p**.

### Distraction Free Mode (alt-shift-enter)
Distraction free mode removes the menu, toolbar and status bar and optionally lets you maximize the the Window to full screen so you can just focus on the editor. 

![](/images/DistractionFreemode.png)

##### Customizing Distraction Free Mode
You can customize how Distraction Free Mode operates by specifying exactly what to hide using a configuration settings in **Tools -> Settings**:

```json
"DistractionFreeModeHideOptions": "menu,toolbar,statusbar,preview,tabs,maximized,maxwidth:970"
```

Each of the keywords specifies corresponds to a UI element to hide except for maximized, which if specified causes the window to maximized.

### Presentation Mode (F11)
Presentation mode shows only the previewer for the editor removing everything else from the Markdown Monster Window.

You can also launch Markdown Monster in Presentation Mode in two ways:

* **Using the `-presentation` Command Line Switch**   
You can launch Markdown Monster with a special command line switch:  
`mm -presentation` or `mm .\docs.md -presentation`

* **Using the `OpenInPresentationMode` Config Setting**  
You also set `"OpenInPresentationMode": true;` setting in the Markdown Monster Settings in the **Tools -> Settings**.

### Managing Whitespace: CenteredLayout and  MaxWidth
When running on wide monitors it might not be desirable to stretch content across the entire edit area, but rather limit the editor text to a certain text width. 

You can toggle Centered Layout from the **View -> Toggle Centered Layout** menu option.

There are two settings that control this behavior in the **Tools -> Settings**:

```json
"Editor": {
    "CenteredMode": true,
    "CenteredModeMaxWidth": 970,
}
```

**CenteredMode** when set causes the content to be centered in the middle of the editor pane if the width of the pane exceeds the `CenteredModeWidth`. Any width in excess of this max width is padded on both sides of the editor text, effectively producing margins for the document.

This allows you to keep a comfortable editing 'column' width for your editor content that isn't so wide that it's difficult to read and edit. The width is configurable and defaults to 970 pixels.

For more info see [Editor Padding and Centered Layout](VFPS://Topic/_5ED0RJ891).