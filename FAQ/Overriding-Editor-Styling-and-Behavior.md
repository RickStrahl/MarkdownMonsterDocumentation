You can override some editor styling features as well as code behavior by creating one of two override files in the `Editor` folder of the Markdown Monster installation:

* **editor-user-extensions.css** - CSS Style overrides
* **editor-user-extensions.js** - JS Editor code overrides
* **.NET Addins** - more sophisticated integration

Both of these options require a bit of inside knowledge about how ACE Editor works and is likely only going to be useful for developers or for customizations suggested by support.


## Style overrides (CSS)
Style overrides let you override the visual aspects of the editor, which uses general ACE Editor styling along with specific editor themes. Any override you make in `editor-user-extensions.css` are applied at the end of the CSS hierarchy so you can override any pre-existing behaviors.

An example might be to remove underlines from hyper links in `[link](https://site.com/hyperlink)` syntax which can be overridden via the `ace_underline` style:

```css
span.ace_markup.ace_underline {
    text-decoration: none;
}
```

## Code overrides (JS)
This is a developer feature  that is likely useful only to a few people who want to tinker with the inner behavior of the editor. You can refer to the editor integration code in `Editor\editor.js` for more insight into how the editor operates. Any override you make in `editor-user-extensions.js` are applied after the other editor scripts have loaded.

Code overrides let you customize the behavior of the editor outside of the Markdown Monster default initialization sequence. This script is fired at the end of the script loading sequence and you can have access to:

* `textEditor` - MM's wrapper around ACE editor
* `textEditor.editor` - ACE Editor instance

Common things that you can do is change editor settings and behavior that you can gleam by looking at the `configureAceEditor()` and `setEditorStyle()` functions in the editor wrapper object. You can gain access to all of these settings through the `textEditor` or `textEditor.editor` instances and customize behavior.

## Markdown Monster Addins (.NET)
To interface with editor **behavior** you will be better off using a Markdown Monster Addin at the host level instead as the host has access to these same objects. There are a number of behaviors exposed that you can hook into using Addins, both via exposed .NET event hooks and editor behavior access.