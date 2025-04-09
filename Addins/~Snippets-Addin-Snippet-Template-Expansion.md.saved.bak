The Snippets Addin allows for Text Template Expansion, optionally enhanced with C# code expressions to dynamically add content to the snippet. Using this tool lets create reusable Text Snippets that you can easily embed into your currently open document. 

Snippets can be:

* Expanded into text from an *Expansion String*
* Triggered by an assignable *Keyboard shortcut*
* Interactively launched from the Snippets Editor

The C# Scripting allows for:

* Expressions - `{{ expression }}`
* Code blocks - `{{% code block }}`
* Editor Selection Text - `@@@`

You can create, manage and execute snippets from the snippet editor which opens from the Addins Toolbar:

![](https://github.com/RickStrahl/ImageDrop/raw/master/MarkdownMonster/SnippetsAddin.gif)

The example demonstrate two common use cases:

* A large static Text Template - a bug report to be filled out
* A helper to create some dynamic content - a FrontMatter header in this case

Other use cases:

* **Preformatted Text Templates**  
If you commonly create new documents or sections in your documents that use the same text, you can create a template that expands this repetitive text from a text template.  
*<small>Examples: A bug template or FrontMatter Blog Header.</small>*

* **Text Transformations**   
Want to create custom markup operations of selected text? You can easily create template expansions that let you expand the current selection.  
*<small>Example: `<div class='note'>@@@</div>`  (`@@@` = active selection)</small>*

* **Embed Dynamic Data**  
If you need to embed dynamic content into your editor you can use C# code to retrieve dynamic content using Handlebars like syntax (`{{ expression }}` and `{{% code block }}`). This an be as simple as embedding the current date or embedding a friendly date, or might be something more complex such as retrieving a version number from a Git repository or other resource and embedding that content into the page.  
*<small>Example: `{{DateTime.Now.ToString("MMMM dd, yyyy - HH:mm tt")}}`</small>*

* **Aid with structured Markup**   
Sometimes it's useful to create shortcuts for more complex Markdown structures such as figure or code captions, icons embedded or commands that might be easy to forget like Mermaid charts or MathMl Markdown wrappers.

## Snippets: Template Driven Text Expansion
Template Expansion has two modes of operation:

* Static Text Expansion
* C# Code Execution

### Text Expansion
The key feature of the Snippets Addin is template text expansion, which simply means that the text of the snippet can be inserted at the current document's editor position. 
#### Plain Text Snippet Examples
Text expansions can be plain text and simply expand text as is into the editor. While this is pretty basic *text copying* operation, it's quite useful for many use cases like pre-defined document templates similar to the Bug Template example in the screen cast.

The following example, is an example of a footer that I use in all of my blog posts. It's an HTML fragment, which is rendered in Markdown as HTML and it's nothing more than a plain text expansion:

```html
<div style="margin-top: 30px;font-size: 0.8em;
            border-top: 1px solid #eee;padding-top: 8px;">
    <img src="https://markdownmonster.west-wind.com/favicon.png"
         style="height: 20px;float: left; margin-right: 10px;"/>
    this post created and published with 
    <a href="https://markdownmonster.west-wind.com" 
       target="top">Markdown Monster</a> 
</div>
```

**Expansion string:**  `cwmm`  

With this snippet setup I can now type `cwmm` into the editor, and as soon as I do, the `cwmm` text is replaced with the expanded template.

![](https://github.com/RickStrahl/ImageDrop/raw/master/MarkdownMonster/SnippetExpansion.gif)

#### Text with C# Expressions
You can also embed C# expressions into your text templates. This allows you to access any C# language features - expressions and even structured code blocks - as well as access Markdown Monster's application Model that gives you access to the current document, the editor, and even the user interface.

The following example snippet creates a FrontMatter blog post header that picks up the current document title and today's date using C# expressions:

```markdown
---
title: {{ Model.ActiveDocument.Title }}
date: {{ DateTime.Now.ToString("yyyy-MM-dd") }}
tags: 
- ~

---
```

**Expansion String:** frontmatter

In this snippet notice the expressions using `{{  }}` to delineate C# expressions that are expanded. Above:

`{{ DateTime.Now.ToString("yyyy-MM-dd") }}`

embeds the date in the format that FrontMatter requires for example. You can also access the `Model` which is [Markdown Monster's Application Model](VFPS://Topic/_67613ZLO8) which gives you access to a number of other objects:

* [ActiveDocument](VFPS://Topic/_67613ZN74)
* [ActiveEditor](VFPS://Topic/_67613ZNKB)
* [JavaScriptInterop](_67613zqba) <small>(low level editor access)</small>
* [OpenDocuments](VFPS://Topic/_67613ZLQF)
* [OpenEditors](VFPS://Topic/_67613ZLQK)

and much more.

You can also invoke methods on various objects. For example you can retrieve the current selection like this:

`{{ await Model.ActiveEditor.GetSelection() }}`


Retrieve the current line number and text:

`{{ await Model.ActiveEditor.GetLineNumber() }}. {{ await Model.ActiveEditor.GetCurrentLine() }}`

> Note that many editor operations are `async` hence the `await` for these calls. But not all methods that can be called require `await` - check the documentation for `Task` results which indicate that `await` is required.

#### Special Characters
There are two special expressions that access common functionality:

* `@@@` - the same as `{{ await Model.ActiveEditor.GetSelection() }}`
* `~` - denotes the location of the cursor after insertion

#### Expanding the Active Selection
A common task that snippets are good for is text expansion of the current selection in the editor. This is similar to the way MM already expands many common operations like Bold, Italic, Lists etc. by taking the current selection and marking it up with additional text for formatting.

The following creates a custom HTML fragment to embed into a Markdown document to display a box using an application specific CSS class. 

```html
<div class='breaking-changes'>{{ await Model.ActiveEditor.GetSelection()}}</div>
```

Because `.GetSelection()` is a common item there's a string shortcut for it in a template using `@@@`. So the following produces the same output:

```html
<div class='breaking-changes'>@@@</div>
```

Note that you can't use a expansion string for these types of text expansions that work of a selection, as a selection has to be active and you can't do that when also typing an expansion string.

### C# Code Execution
Snippets support full C# program creation using the script syntax which is based on Handlebars using `{{ }}` brackets. Two types of code execution are supported:

**Expressions**  

```
{{ Model.ActiveDocument.Filename }}
```

```
<sub>{{ await Model.ActiveEditor.GetSelection() }}</sub>
```

**Simple Code Blocks**  

```
{{% 
var wc = new WebClient(); 
var version=wc.DownloadString"("https://west-wind.com/files/MarkdownMonster_Version.xml"); }}`
}}
```

**Structured Code Blocks**  

```
{{% if(true)  { }}
    true
{{% } else { }}
    false
{{% } }}
```

> #### Async Support
> Expressions and code block support are execute in an `async` context, so you can use `await` to call async methods from your expressions and code block. Note that **most operations that affect the text editor async**. For example `{{ await Model.ActiveEditor.GetCurrentLine() }}`.

#### How Code Execution works
Any code expressions and code blocks are expanded by compiling into an executable method that is dynamically invoked - the entire snippet is essentially turned into a text generating output method that returns a string.

Text is transformed into string literals that are written into the output stream, and expressions `{{ }}` are inlined into the and evaluated between these text literals.

Code Blocks `{{% }}` are raw C# code blocks that are generated as raw C# commands into the generated code output. 

#### Examples of Code Execution
Let's look at a few examples.

The first example, is a small example that uses a bit of C# code to dynamically download the latest version number for Markdown Monster from the Internet and embeds it into a string to be embedded.

**Code Block and Expression**

```cs
{{%
var url = "https://west-wind.com/files/MarkdownMonster_version.xml";

var wc = new WebClient();
string xml = wc.DownloadString(url);
string version =  StringUtils.ExtractString(xml,"<Version>","</Version>");
}}
# Markdown Monster v{{version}}
```

The result of this script is a string and the value is the Markdown Monster version header:

```markdown
# Markdown Monster v2.5.4
```

This means you can write:

* C# Expressions (single values or method calls)
* C# Code Blocks (single self-contained block of code)
* C# Structured Statements (`if`, `for`, `while` etc. with text or expressions or other code in between)    
*<small>Structured statement blocks can embed other text or single expressions, but can not embed additional nested code blocks.</small>*

We haven't seen the last item yet - the code above uses a single block of C# code to handle the Web retrieval.

Structured statements tend to be conditional or iteration commands like `if`, `for` or `while` that have a start and end bracket.

The following example is contrived: It displays a list of all the open documents in Markdown Monster and it uses `foreach()` to do so.

**Structure Code Blocks**

```cs
{{% 
int count = 0;
foreach(var document in Model.OpenDocuments) 
{
   count++;
}}

{{count}}. {{ Path.GetFileName(document.Filename) }}

{{% } }}
```

This produces a list of open documents like this:

```text
1. Changelog.md

2. Readme.md

3. Todo.md
```

> Note that whitespace is tricky with Structure Code Blocks because the `}}` and any following space/line break is part of the rendered template.  This means if you want a tight list the actual command looks like this:

```cs
{{% 
int count = 0;
foreach(var document in Model.OpenDocuments) 
{
   count++;
}}{{count}}. {{ Path.GetFileName(document.Filename) }}
{{% } }}
```

```text
1. Changelog.md
2. Readme.md
3. Todo.md
```

### Debugging Templates in Interactive Mode
If you are creating templates with C# code, it's very likely that you might create some errors in the expressions or code blocks you use. Maybe you're using the wrong name for a object, property or method or maybe your logic simply has a type or missing symbol.

Luckily you can run your templates interactively in the Snippets Form by selecting your snippet and clicking on the **Test Snippet** button. This runs the snippet but rather than embedding the result into the document the snippet is displayed in a dialog:

![](/images/SnippetsAddin.png)


If an error occurs a dialog is displayed with the compilation error along with the generated source code, so you can review the code if the message on its own is not obvious:

![](/images/SnippetsAddinErrors.png)

### Using the API Documentation to Access Markdown Monster Features
If you're using the C# features to access functionality in Markdown Monster you'll want to definitely take a look at the documentation site:

* [Main Documentation Site](https://markdownmonster.west-wind.com/docs)
* [API Documentation](https://markdownmonster.west-wind.com/docs/_55o1dxzia.htm)

Some key object you'll likely want to access:

* [ActiveDocument](VFPS://Topic/_67613ZN74)
* [ActiveEditor](VFPS://Topic/_67613ZNKB)
* [JavaScriptInterop](_67613zqba) <small>(low level editor access)</small>
* [OpenDocuments](VFPS://Topic/_67613ZLQF)
* [OpenEditors](VFPS://Topic/_67613ZLQK)