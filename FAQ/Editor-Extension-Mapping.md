Markdown Monster supports a number of different editor syntax formats, and you can edit documents in any of these formats. Many default file formats like - `.js`, `.html`, `.css`, `.ts`, `.cs`, `.json`,`.config` etc. - are supported out of the box.

### Adding Custom Extensions
The extensions are mapped in the `EditorExtensionMappings` settings inside of the configuration file at:

```dos
%appdata%\Markdown Monster\MarkdownMonster.json
```

Editor extensions are stored as key value pairs with the extension as the key, and the editor format as the value:

![](/images/EditorExtensions.png)

To access this file use **Tools -> Settings -> Edit Json -> EditorExtensionMappings**. To add a custom extension, simply add another key and value:

```json
  "EditorExtensionMappings": {
    "myext": "markdown",
    "md": "markdown",
    "markdown": "markdown",
    "mdcrypt": "markdown",
```

which specifies I want files with a `.myext` extension mapped to edit with `markdown` syntax in the editor.

The format or value in the map above refers to an ACE editor syntax found in the `editor\scripts\Ace\mode-*.js` folder. Any of the modes listed there can be mapped to a custom extension.