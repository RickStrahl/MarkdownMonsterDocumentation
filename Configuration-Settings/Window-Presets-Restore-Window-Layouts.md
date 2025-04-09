Markdown Monster has a configurable Window Presets drop down on the title bar, that allows you to quickly select a preset window size that customizes the window's width and height, and the size of the preview and the sidebar panes. 

![](/images/WindowPresetDropdown.png)

This allows you to quickly access previously saved window configurations which are made up of window height and width, and sizes for the Preview and Sidebar panes. A default list is provided and you can create your own presets by either adding a current size/view, or manually editing the values in the configuration file

Here's what the features look like:

![](https://github.com/RickStrahl/ImageDrop/raw/master/MarkdownMonster/WindowPresets.gif)

## Selecting Window Sizes
You can simply click on the Window down button next to the Window's control box to see a list of currently defined presets. Select and click on any of the presets to set your window to the selected size. 

> If you select a window that is to large, or would render offscreen at current position the Window may resize itself so it fits on your currently active screen.

## Saving your Current Window Layout
You can add new positions to the Window layout using the **Add Current** menu option on the bottom. The option shows the current size of the window and preview and sidebar panes.

## Manually Editing Presets in the Configuration File
The list of presets is stored in the configuration file, which you can quickly access by clicking on the **Edit Presets in Configuration** menu item.

This opens the editor and shows a list that looks something like this:

```json
"WindowPresets": [
  "2500 x 1750,1050,350",
  "2250 x 1500,920,330",
  "1900 x 1020,730,310",
  "1600 x 850,600,300",
  "1250 x 760,445,270",
  "950 x 620,445,0",
  "770 x 560,380,0",
  "1425 x 937, 747, 300"
]
```

The list contains three separate values:

* Window Width x Window Height
* Preview Pane Width
* Sidebar Width (set to 0 to hide)

You can add and remove entries here, or edit existing ones.

Any changes you make in the Markdown Monster Editor are immediately reflected in the Preset list the next time you use it.

> If you edit the values in an external editor, changes require a restart of Markdown Monster. MM may also overwrite your settings as the application shuts down and writes out the current configuration. So if you use an external editor preferably save after MM has shut down.