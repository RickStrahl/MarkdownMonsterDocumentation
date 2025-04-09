Markdown Monster by default uses **global configuration** settings that are stored in `%appdata%\Markdown Monster\markdownmonster.json`. These global settings can be set directly in the JSON configuration file, via the Configuration Settings window, or by setting various values in the User interface via menu or status bar options.

The global settings apply to all open documents and folders and projects and for the most part the single set of global settings are sufficient. But in some cases you might want to use **different settings** for a particular project or files located in a specific subfolder. For example, you might want to apply separate Markdown parsing features in a specific project or folder, or use custom PreviewTheme for a specific project or folder.

### Customizing Global Settings by Project or Folder
You can override the global settings in one of two ways:

* **.markdownmonster` Folder File**  
This file in the root of a project applies overridden settings **to all files in the current folder and downward hierarchy**. 

* **Markdown Monster `.mdproj` Project File**   
When you have a Markdown Monster project open, the overridden settings you set here are applied **to all open files** until you close the project.

### The .markdownmonster Folder File
You can place a `.markdownmonster` file into the root folder of a project. If you place an empty file, that file marks the 'rendering root' of the project that is checked for path resolution when referencing URLs in documents with `/` or `~/` start paths. MM searches up the hierarchy to check for the `.markdownmonster` file and if it finds it uses the folder it lives in as the project root for root folder resolution.

In addition, you can also place **JSON configuration values** into this file. Using keys that map the same structure as found in the `markdownmonster.json` configuration file you can **override any settings** from the base global configuration.

For example you can override themes and font information like this in `.markdownmonster`:

```json
{
    "EditorTheme": "vscodelight",
    "PreviewTheme": "Blackout",
    "Editor": {
      "FontSize": 18,
      "PrintMargin": 80,
      "ShowPrintMargin": true
    },
    "Markdown": {
        "GenericAttributes": true,
        "SmartyPants": true
    }
},
```


You can override any root object properties and any of the properties in the `Editor` and `Markdown` sub-configurations. All other settings are ignored as they are global in nature.

> #### @icon-warning .markdownmonster Configuration: Folder Scope
> The `.markdownmonster` marker file settings are **applied only to files in the hierarchy at or below the folder level of the `.markdownmonster` file.** Files loaded outside of the file hierarchy use the global, non-overridden settings.

Here's what this looks like:

![](https://github.com/RickStrahl/ImageDrop/raw/master/MarkdownMonster/HierchicalSettings.gif)


### Configuration Settings an .mdproj Project File
If you open an `.mdproj` Project file in Markdown Monster you can apply custom configuration settings via the `.mdproj` file and it's JSON `.Configuration` key. Any values applied override the same values in `markdownmonster.json` from the global configuration.

To configure custom settings, add a `Configuration` JSON key to the root object in the `.mdproj` file:

```json
"Configuration": {
    "EditorTheme": "vscodelight",
    "PreviewTheme": "Blackout",
    "Editor": {
      "FontSize": 18,
      "PrintMargin": 80,
      "ShowPrintMargin": true
    },
    "Markdown": {
        "GenericAttributes": true,
        "SmartyPants": true
    }
},
```

You can override any root object properties and any of the properties in the `Editor` and `Markdown` sub-configurations. All other settings are ignored as they are global in nature.

> #### @icon-warning Project File Configuration: All Open Files Scope
> The custom settings only work when the project is open in Markdown Monster. While the project is open **all open files use the overridden configuration settings**. Global settings are applied when you close the project.


### Override Behavior: No UI - JSON Settings Only
Both of these configuration overrides are applied **ontop of the global settings**, and the values **can only be set in the configuration files not through the User Interface**. The User Interface only shows the global values, and if you change any of the values in the User Interface only the global values are updated, but which won't have any effect on any overridden values from the custom configuration.

### Settings May Reqiure Reloading or Reactivating Documents
Most settings are applied as soon as you set them and save the JSON file. A few settings however may require that explicitly re-activate the document either by switching document tabs or reloading the document.

There are a few settings that can't be changed. For example, you can't change the full application theme in this way as theme changes require a restart. Editor and Preview Theme changes work fine however and are immediately reflected.