If you're generating output for PDF or printing, you may need to generate Page breaks in your documents. Markdown doesn't direct support for Page Breaks but you can use HTML to force a page break using the following markup:

```html
<div style="page-break-after: always"></div>
```

Since Markdown supports embedded HTML rendering, this forces a page break into a printed or PDF document.

You can just type the text above into your document, but Markdown Monster also includes a couple of shortcuts to get this HTML into the page without having to remember this verbose syntax:

* Using the Toolbar Dropdown Page Break option
* Using a custom `pagebreak` snippet expansion

![](/images/PageBreakExpansion.gif)


### Page Break Toolbar Dropdown
You can find the Page Break Toolbar Drop down on the extended toolbar menu that drops down at the end of the editor operations list:

![](/images/PageBreakToolbarDropdown.png)

### Creating a `pagebreak` Snippet Expansion
Markdown Monster includes a Snippets add in which allows for creating custom text expansions that can be embedded either explicitly by using the snippet editor, or by typing a key sequence that a give snippet is assigned to.

You can create a new snippet called `pagebreak` as shown in the image below. Once created, you can run the snippet by pressing the play button in the Snippet Editor.

Or, more commonly: You can simply type the `pagebreak` expansion string into your document. The snippet is configured to expand into the page break HTML shown above at your cursor position.

![](/images/PageBreakTemplateExpansion.png)