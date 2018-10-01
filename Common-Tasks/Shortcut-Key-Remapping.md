Markdown Monster has the ability to remap many of it's shortcut keys that are defined on menus and elsewhere.

Key mappings can be changed by re-mapping shortcut keys in:

```dos
%appdata%\Markdown Monster\MarkdownMonster-KeyBindings.json
```

> #### @icon-info-circle KeyBinding Changes Require Restart
> When you make changes to key bindings in `MarkdownMonster-KeyBindings.json` you have to restart Markdown Monster to see the changes applied.

### Key Mappings
The key mappings are defined as a pair of properties that map a **shortcut key** to a **command name**. The `CommandName` is fixed and you can change the `Key` property to change the behavior.

The format of the file is in JSON and it looks like this:

```json
[
  {
    "Key": "alt+shift+return",
    "CommandName": "DistractionFreeMode"
  },
  {
    "Key": "f11",
    "CommandName": "PresentationMode"
  },
  {
    "Key": "ctrl-n",
    "CommandName": "NewDocument"
  },
  {
    "Key": "ctrl-o",
    "CommandName": "OpenDocument"
  },
  {
    "Key": "ctrl-s",
    "CommandName": "SaveDocument"
  },
  {
    "Key": "ctrl-shift-s",
    "CommandName": "SaveAs"
  },
  {
    "Key": "alt-shift-s",
    "CommandName": "SaveAll"
  },
  
  {  more keys... }
}  
```

To make a change, find the command (or key) that matches the operation you want to change and change the key.

### Resetting the Default Key Mappings
To reset the original key mappings in Markdown Monster, delete the `MarkdownMonster-KeyBindings.json` file. This causes Markdown Monster to use the default bindings, and re-create the file with the default bindings.

### Shortcut Key Format
There are a number of rules that apply to these short cut keys.

* There's no support for key *chords* - only a single key and modifier combination can be used

* If there are duplicate key definitions, last one defined wins as it will remap a previous assignment.

* Not all key combinations will work


### Not all Key Combinations Work
Markdown Monster manages keybindings both as part of the WPF application that runs the main application, as well as the editor which uses JavaScript and the ACE Editor. 

There is some overlap between the Editor and the host application and some key combinations can fire in the editor first where they may not be captured. This can result in some keystrokes getting intercepted in the browser and not firing the way you'd expect. 

However, most mappings should work, but just be aware that some key combinations may not work.




