Markdown Monster has the ability to remap many of it's shortcut keys that are defined on menus and elsewhere.

Key mappings can be changed by re-mapping shortcut keys in:

```dos
%appdata%\Markdown Monster\MarkdownMonster-KeyBindings.json
```

> #### @icon-info-circle KeyBinding Changes Require Restart
> When you make changes to key bindings in `MarkdownMonster-KeyBindings.json` you have to restart Markdown Monster to see some of the changes applied.

### Key Mappings
The key mappings are defined as a pair of properties that map a **shortcut key** to a **command name**. The `CommandName` is fixed and you can change the `Key` property to change the shortcut key.

The format of the file is in JSON and it looks like this:

```json
[
  {
    "Id": "NewDocument",
    "Key": "Ctrl+N",
    "CommandName": "NewDocument",
  },
  {
    "Id": "OpenDocument",
    "Key": "Ctrl+O",
    "CommandName": "OpenDocument",
  },
  {
    "Id": "CloseActiveDocument",
    "Key": "Ctrl+F4",
    "CommandName": "CloseActiveDocument",
  },
 
  
  //  more keys...
]  
```

To make a change, find the command (or key) that matches the operation you want to change and change the key.

### Editor Commands 
You can also map specific Editor Commands. These commands are the default commands that Markdown Monster supports plus any Editor Commands that Addins can add as part of their processing. Markdown Monster internally maps most of the common editor commands which are the ones you see on the toolbar.

Editor commands look like this:

```json
[
 {
    "Id": "EditorCommand_Softbreak",
    "Key": "Shift+Enter",
    "CommandName": "EditorCommand",
    "CommandParameter": "softbreak"
  },
  {
    "Id": "EditorCommand_Bold",
    "Key": "Ctrl+B",
    "CommandName": "EditorCommand",
    "CommandParameter": "bold"
  },
  {
    "Id": "EditorCommand_Href",
    "Key": "Ctrl+K",
    "CommandName": "EditorCommand",
    "CommandParameter": "href"
  },  
  // ... 
]
```

> Note that editor commands all use the same `"CommandName": "EditorCommand"` and **require** a unique Id that starts with `EditorCommand_`. If you created custom commands (shown below) make sure you use this same convention.
  
There are also various Editor Commands that don't have short cuts, namely those on the 'extended menu because they are by definition 'extended' and not so frequently used values. However those can be also mapped by setting the `CommandParameter` to the appropriate editor update command like this:

```json
{
    "Id": "EditorCommand_BoldItalic",
    "Key": "Ctrl+Shift+B",
    "CommandName": "EditorCommand",
    "CommandParameter": "bolditalic"
},
{
    "Id": "EditorCommand_Small",
    "Key": "Ctrl+Shift+S",
    "CommandName": "EditorCommand",
    "CommandParameter": "small"
}
```  

This works for Editor Commands that aren't mapped:

* small
* bolditalic
* underline
* pagebreak
* lowercase
* uppercase
* mark

as well as for custom commands that an addin can implement and handle in the [MarkdownMonsterAddin.OnEditorCommand()](VFPS://Topic/MarkdownMonsterAddin.OnEditorCommand) method.

### Custom HTML and Template Commands
You can also add custom commands

* `html|tag`  - wraps selected text with HTML tag
* `html|<mytag>{0}</mytag>` - template where {0} is expanded to the selected text

```json
{
    "Id": "EditorCommand_Small",
    "Key": "Ctrl-Shift-S",
    "CommandName": "EditorCommand",
    "CommandParameter": "html|cite"   // <cite>selected text</cite>
},
{
    "Id": "EditorCommand_AlertBox",
    "Key": "Ctrl-Shift-A",
    "CommandName": "EditorCommand",
    "CommandParameter": "html|<div class=\"alert alert-warning\">{0}</div>"
}
```

> If implemented here only, the commands will have no menu or toolbar buttons associated with it. If you want to add UI you can use [Additional Commands and Icons on the Toolbar](VFPS://Topic/_5IM10BJPW).

### Resetting the Default Key Mappings
To reset the original key mappings in Markdown Monster, delete the `MarkdownMonster-KeyBindings.json` file. This causes Markdown Monster to use the default bindings, and re-create the file with the default bindings.

### Shortcut Key Format
There are a number of rules that apply to these short cut keys.

* There's no support for key *chords* - only a single key and modifier combination can be used

* If there are duplicate key definitions, last one defined wins as it will remap a previous assignment.

* Not all key combinations will work


### Not all Key Combinations Work
Markdown Monster manages keybindings both as part of the WPF application that runs the main application, as well as the editor which uses JavaScript and the ACE Editor. Whenever possible we try to use JavaScript editor keys when commands are editor specific, and WPF keys when the commands are shell based or affect non-editor behavior.

There is some overlap between the JavaScript editor and the host application and some key combinations can fire in the editor first or in WPF first which may result in keys not firing as expected. Most mappings should work fine, just be aware that some key combinations may just not work or not work as expected - be prepared to choose a different key combination in that case.