#### Font
The name of the font to use in the editor. The font used **has to be a monospaced font** like **Consolas** (default), **Courier New**, **Lucidia Console** or installed monospace fonts like **Fira Code**, **Haskell** etc. Using proportional fonts likw Segoe UI, Arial, etc. doesn't work and will cause cursor offset issues. You can also use `monospace` which will default to the default monospace font (usually Courier New) for Internet Explorer. For more info please the [Font Support](VFPS://Topic/_5EA0SD8QX) topic.

#### FontSize
Font size in pixels and the default size is 18.

#### LineFeedMode
Determines how new lines are handled by the editor for copy and paste operations and any new text that is entered. Valid values: `Lf` and `CrLf`. Unix style `Lf` is the default.

#### ZoomLevel
The Zoom level is a percentage value (100 is 100%, 50 is 50%) that is a multiplier on the font size. This value is dynamically updated from `ctrl-scrollwheel` or `ctrl-+` and `ctrl-_` operations. This is mostly for internal use, but you can set it to 100 to clear the zoom level.

#### LineHeight
The line height determines the amount of space including white space that that a single line of text takes up. Sizing is in relative units and the default value `1.35`.

#### Padding
You can sepecify the padding for the editor's editing surface. This value is a fixed pixel value and cannot be specified as a percentage. If **MaxWidth** it will override the **Padding** value once the width exceeds the **MaxWidth**

#### MaxWidth
You can specify a max width for the editor content to keep content from spreading over the whole width of the editing area when using very wide screens. **MaxWidth** can be used to provide a managable edit 'column width' and provide extra wide space for a pleasant, distraction free experience. A *maxwidth:1000* setting can also be applied to the **DistractionFreeModeHideOptions**.

#### EnableBulletAutoCompletion
Determines whether Markdown bullet auto-completion is enabled. This behavior automatically creates new bullets on enter. Default is false as the behavior can be annoying when using short lists and automatically generating an extra bullet on the last item that needs to be deleted.

#### HighlightActiveLine
Determines whether the active line in the editor is highlighted. Highlight color is relatively subtle in most themes so this is recommended.

#### EditorWrapText
Determines whether text in the editor wraps - almost certainly you'll want to leave this flag at `true`.

#### EnableSpellCheck
Toggles the spellchecking feature in the editor. This flag is also triggered by the checkmark icon on the Window control box.

#### AllowScriptTags
Determines whether script tags are rendered into the HTML as is (as raw HTML script) or are encoded and stripped for security. Set to `true` if you want to embed script tags explicitly (like Gist Snippets or other Widgets for example).

#### TabSize
The number of spaces added by pressing the Tab key.

#### WrapText
Determines whether text wrapping is enabled. Set with the default of Alt-Z shortcut and on View menu.

#### WrapMargin
Optional margin at which text is wrapped. Default is 0 which means it wraps at the document's natural width. If you specify a value the editor wraps at that column.

> Note this setting may cause extra whitespace on the right side of the editor. If `MaxWidth` is set and the wrap margin is smaller the content will not be centered any more.

#### ShowPrintMargin
Shows a print margin marker line on the right side of the document at the given margin. This can be useful in some cases to see how wide text is at a given location.

#### PrintMargin
Configures a numeric margin value where the print margin in `ShowPrintMargin` is displayed.

#### Dictionary
The dictionary used. By default the US English one is used by `de-DE`, `fr-FR` and `es-ES` are also shipped. You can add any other OpenOffice compatible dictionaries using `aff` and `dic` files and reference them here by copying them into the `Editors` folder. [More info](VFPS://Topic/_4TE0RA79S).

#### KeyboardHandler
Allows you to set keyboard themes. Supported values are:
    * default
    * vim
    * emacs

#### PreviewHighlightTimeout
Determines how long the preview highlight is highlighted in the Previewer. In milliseconds. Set the value to 0 to always leave it highlighted. The highlight is triggered whenever the preview refreshes which is upon clicking, when the document changes, or when you navigate with the arrow keys (note: *Vim and Emacs navigation keys do not trigger preview updates*)