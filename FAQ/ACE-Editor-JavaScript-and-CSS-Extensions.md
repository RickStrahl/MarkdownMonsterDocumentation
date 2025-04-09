The editor in Markdown Monster uses <a href="https://ace.c9.io/" target="top">ACE Editor</a> and you can extend the editor behavior by adding some JavaScript to the editor. This is useful for Addin authors or those creating Commander Addin scripts.

You can extend the editor by creating:

* JavaScript Code in  `Editor\editor-user-extensions.js`
* CSS styling in `Editor\editor-user-extensions.css`

### ACE Editor Access from Markdown Monster
To access the ACE Editor wrapper in Markdown monster you use the `MarkdownDocumentEditor` instance which is accessible via `Model.ActiveEditor.AceEditor`. 

There are two ways to interact with the JavaScript interface:

* Use the .NET Helpers on `MarkdownDocumentEditor`
* Use the MM JavaScript wrapper object
* Use ACE Editor's API directly

### Use the .NET Wrappers
The `MarkdownDocumentEditor` class has a number of methods that perform a few common operations on the editor. You can retrieve and set selections, you can search the document, get and set the cursor and scroll positions, replace content, restyle the editor, toggle a number of options and so on. Check the class interface on `MarkdownDocumentEditor` for what's available.

### Use the JavaScript Wrapper
Markdown Monster uses a fairly large wrapper interface to interact with ACE Editor. All interaction with ACE is driven through this interface which is both used internally from JavaScript, but is also accessible to call from .NET via the `Model.ActiveEditor.AceEditor` instance. 

`AceEditor` is the JavaScript object map that provides a host of editor operations and internal interaction, which is defined in `editor.js`. This is considered internal code, but addins and Commander snippets can take advantage of this functionality as well if you're willing to do some digging into the JavaScript code.

To access this object from .NET code you can use code like this:

```cs
var range = Model.ActiveEditor.AceEditor.GetSelectionRange(false);
```

> #### @icon-warning Parameterless JavaScript Functions require a single Parameter
> Parameterless functions called via interop on the AceEditor instance have to pass a single parameter - typically `false` - to allow the interop call to succeed. This is a quirk of COM->JavaScript interop in .NET and since you're calling directly into JavaScript without a wrapper this is required. The above method has no parameters but `false` is passed, otherwise the call fails. If methods have parameters, just parameters that you would normally pass.

### Extending Editor Functionality
Markdown Monster lets you extend the editor via a custom script file you can create in:

* `<installDir>\Editor\editor-user-extensions.js`

This file is loaded into the editor if it exists, but unlike other files, this file is not shipped with Markdown Monster nor updated in update releases, so the file stays customized with your changes.

In this file you can extend the `window.textEditor` object and add methods of your own:

```javascript
var te = window.textEditor;

te.helloWorld = function(message) {
  alert("Hello...\n" + message);
}
```

You can then call this function from .NET code with:

```cs
Model.ActiveEditor.AceEditor.helloWorld("Customizing ACE Editor");
```

### Access ACE Editor Directly
You can also access the raw ACE Editor instance directly via:

```cs
var ace = Model.ActiveEditor.AceEditor.editor;
```

or in JavaScript code in `editor-user-extensions.js`:

```javascript
var ace = window.textEditor.editor;
```

Using this instance you can access all of ACE's features defined by the ACE Editor API directly. Note that the preferred approach is to create a JavaScript wrapper function and call that from .NET rather than accessing the editor directly to keep the interface less chatty and to avoid parameter passing conflicts.

### Things to watch out for

#### ACE Editor Instantiation
The ACE instance is not immediately initialized when the document loads. Instead ACE is initialized when the .NET component loads the document and then calls it with configuration information to properly apply styles and options. For this reason code like this will not work:

```js
var te = window.textEditor;  // works
var aceEditor = te.editor;   // ACE instance - null, not initialized yet

te.myFunction = function() {
    var aceEditor = te.editor;  // this works - ACE doc instance
}
```

> #### @icon-warning Do not use Reserved Global Variable Names
> There are several reserved variable names from ACE Editor and the Markdown Monster JavaScript interfaces.
>
> Do not use any of these variable names in your code:
> * **ace**
> * **textEditor**
> * **spellcheck** and **sc**


#### Passing Parameters to and from JavaScript
Although COM supports two-way calls of .NET -> JavaScript and JavaScript -> .NET, there are a few complications to watch out for.

#### Parameterless Functions
Any functions that don't have parameters have to pass a single parameter in spite of the method's parameterless signature. This is due to the way JavaScript objects expect parameters to be passed (via a parameter array) and the way COM handles this. Pass `false` as a parameter to a parameterless function.

#### Object Serialization
Not all parameters can marshal between .NET and JavaScript and it's best to stick to simple types rather than objects. If you do pass objects either use structures or objects that don't have custom methods. Alternately you can serialize parameters to JSON and deserialize as part of the wrapper methods you create. The latter is the most reliable for passing objects back and forth. If at all possible use simple types for parameters.

### Adding ACE Editor CSS Customizations
ACE editor can be customized to some degree using CSS to affect how portions of the editor display and behave. 

You can extend or override default styling by creating a new file in:

* `Editor\editor-user-extesnsions.css`

This file is loaded if it exists and is not overridden during MM updates.

Inside of this CSS file you can apply custom styling to affect MM styling. 

For example:

```css
.ace_cursor { 
    border-left: 4px solid !important;
}
.ace_emphasis {
    font-style: italic;
    font-weight: 600;  
    color: gold !important;
}
```

#### Custom CSS and ACE Themes
Note that many of ACE Editors formatting options come from the various editor themes so if you are making major changes it's probably better to create a new ACE Editor theme. Also realize making changes like colors are either overriding theme colors which may not look right when applying another theme. 

Therefore it's best to minimize the changes you make here to behaviors (like the cursor, or highlights etc.).

If you want to make major changes to a specific theme consider copying an existing theme (in `Editor\scripts\Ace\theme-*.js` files) by copying and extending and renaming an existing theme. If you rename your new theme the theme will be preserved during MM updates.