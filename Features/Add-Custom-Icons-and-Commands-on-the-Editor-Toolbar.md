The Editor toolbar at the top of the Window allows embedding of common Markdown markup on the selected text. The toolbar is kept relatively simple and so it doesn't wrap all operations that are supported. 

It's possible to extend the toolbar with custom operations:

* Adding additional built-in commands
* Adding custom HTML markup commands


You can do this by using the `Configuration.Editor.AdditionalToolbarIcons` which is a collection of an icon name plus a an action name. For example:

```json
"Editor": {
    "AdditionalToolbarIcons": {
      // internal MM Editor Commands
      "Pencil": "mark",
      "ArrowDown": "small",
      // html tag wrapping
      "Coffee": "html|cite",
      // template for text selection
      "Bolt": "html|<b><i>{0}</i></b>"
    },
```

![](/images/AddCustomIcons.png)

The item in each map is a **FontAwesome Icon** to be used as an icon, the second is the name of an existing command. The last (Coffee) example, uses `html|cite` as the value which results in custom tag created around the text as `<cite>text</cite>`.

### Built-in Commands 
Built in commands handle the visible toolbar operations, plus a few additional ones that are not actually shown on the toolbar. The following 3 commands are not already on the toolbar:

* `small` - adds text in `<small>txt</small>`
* `mark` - adds textin `<mark>txt</mark>`
* `numberedlist` - formats lines of text as a numbered list
* `pagebreak` - inserts an HTML pagebreak into the document

All available commands can be found in the source code in:

[MarkdownDocumentEditor::MarkupMarkdown()](
https://github.com/RickStrahl/MarkdownMonster/blob/master/MarkdownMonster/_Classes/MarkdownDocumentEditor.cs#L508)

> You can also create custom addins that extend the default markup 'commands' by implmenting [MarkdownMonsterAddin.OnEditorCommand](VFPS://Topic/MarkdownMonsterAddin.OnEditorCommand) and creating your own commands.

### Custom HTML Tag Wrapping
You can also create a custom HTML commands that wrap the selected text into an HTML element tag. For example:

```json
"AdditionalToolbarIcons": {
   "Pencil": "html|cite"
}
``` 

```html
<cite>selected text</cite>
```

This gives you access to formatting just about any HTML markup.

### Template Content
Additionally you can also create custom HTML output using a simple 'wrapping' template where you use `{0}` to signify the selection.  For example:

```json
"AdditionalToolbarIcons": {
    "Bolt": "html|<b><i>{0}</i></b>"
}
```

Which renders:

```html
<b><i>selected Text</i></b>
```

### Custom Operations
If you need to add toolbar buttons with more control you can also use either the [Commander Addin](https://github.com/RickStrahl/Commander-MarkdownMonster-Addin) or a [full Addin](VFPS://Topic/_4NB0SE717).


```cs
// Font Awesome Icon
public void AddEditToolbarIcon(string iconName, string markdownActionCommand, 
                               ToolBar toolbar = null, ICommand command = null )
                               
// Image Source Icon (sized to 16 high)
public void AddEditToolbarIcon(ImageSource icon, string markdownActionCommand, 
                               ToolBar toolbar = null, ICommand command = null)
```        
                         
For example using the Commander Addin you could use the following:

```cs
Model.Window.AddEditToolbarIcon("Microphone", "html|speak");
```

which can be triggered off a hotkey (or by running the script).

Using a full addin gives you the added capability of loading icon on application startup without requiring an explicit hotkey.

> Note: You can also pass completely custom commands to the `AddEditToolbarIcon()` method using an addin so you can completely take over custom button processing.