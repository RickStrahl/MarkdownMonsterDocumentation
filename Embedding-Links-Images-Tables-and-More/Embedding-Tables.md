Markdown Monster includes a **Table Editor** that makes it easy to create Markdown table content more interactively.

### Main Features

* Support for **Pipe**, **Grid** and **Html** tables
* Two-way editing - edit existing Markdown tables in editor
* Open from Markdown Editor, Clipboard, JSON, CSV
* Re-format existing Markdown tables
* Interactive cell editing
* Live preview of rendered table
* Formatted Markdown or Html output (up to certain column widths)
* Edit table using current preview theme

### Navigation Features
* Tabbable interface - use tab and arrows to navigate
* Auto-inserted rows using tab after last item
* Easy to insert and delete rows and columns
* Sort and align columns
* [Keyboard shortcuts](#keyboard-shortcuts) for navigation and insertions

![](https://github.com/RickStrahl/ImageDrop/raw/master/MarkdownMonster/MarkdownMonsterTableEditor.gif)

### Screen Shots
Here's what the Table Editor looks like:

![](/images/tableeditor.png)

You can also edit tables once they've been created and re-open them in the editor to add content or simply reformat them.

![](/images/editintableeditorcontextmenu.png)

While editing a table you can use the Toolbar or Context menus to manipulate the table contents by adding and removing columns:

![](/images/tableeditorcontextmenu.png)

Notice that the table editor matches your current Preview style. Here I'm using the dark `Blackout` theme, whereas the first screen shot used the `GitHub` preview theme.


> ##### @icon-info-circle Tip: Use the Windows Context Key + Menu Shortcut
> You can use the Windows Context key (usually next to the right Alt key) to bring up the context menu without taking your hands of the keyboard. Each of the context menu options have shortcut keys to jump to the actions quickly    
(**A**bove, **B**elow, **D**elete Row, **L**eft, **R**ight, De**l**ete Column).

> #### @icon-info-circle Reformat a Table
> Want to quickly fix formatting for a pipe or grid table? You can use the **Edit Table** option to open an existing table, open it in the editor, then immediately re-save it and it will be properly formatted (size permitting)
>
> ![Table Reformatting](https://github.com/RickStrahl/ImageDrop/raw/master/MarkdownMonster/FormatTable.gif)

### Data Entry
The first row of the table is considered the **Header** and it is required! The first row is **always** the header for the table.

Any subsequent rows are standard row content and you can have as many rows and columns as you'd like to use. 

When new columns are added new columns are automatically sized to equal widths in the edit table. Actual rendered HTML output will auto-size to accommodate whatever content is used.

### Table Types
The table editor can generate Markdown compatible output to:

* [Pipe Tables](https://help.github.com/articles/organizing-information-with-tables/)

```markdown
| Right | Left | Default | Center |
|------:|:-----|---------|:------:|
|   12  |  12  |    12   |    12  |
|  123  |  123 |   123   |   123  |
|    1  |    1 |     1   |     1  |
```

* [Grid Tables](http://pandoc.org/MANUAL.html#extension-grid_tables)

```markdown
+---------------+---------------+--------------------+
| Fruit         | Price         | Advantages         |
+===============+===============+====================+
| Bananas       | $1.34         | - built-in wrapper |
|               |               | - bright color     |
+---------------+---------------+--------------------+
| Oranges       | $2.10         | - cures scurvy     |
|               |               | - tasty            |
+---------------+---------------+--------------------+
```

> #### @icon-warning Watch for `|` in Markdown Content for Pipe and Grid Tables
> Because the `|` is the column separator in Pipe and Grid tables, using the `|` in actual content as-is doesn't work, because it is construed as a column separator. 
>
> Any literal `|` characters you want to use in Markdown content (in the Markdown text editor) **have to be encoded using `\|`**. However, when using the table editor the `|` is automatically encoded and decoded so that inside of the table editor you should only use `|` instead of `\|`.


* **HTML Tables**

```html
<table>
<thead>
	<tr>
		<th>Header 1</th>
		<th>Header 2</th>
		<th>Header :</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>Column 1</td>
		<td>Column 2</td>
		<td>Column 3</td>
	</tr>
	<tr>
		<td>Custom Table Content</td>
		<td>Column 4</td>
		<td>Column 5</td>
	</tr>
</tbody>
</table>
```

> #### @icon-warning Markdown Support for Tables
> Not all Markdown parsers support all table syntax schemes. GitHub supports Pipe tables and HTML tables only for example, but it all depends on the target platform that is rendering the Markdown text.

### Pipe and Grid Table Column Alignment
Markdown Tables support column alignment 'hints' in the table header columns. You can use the table editor's content menu to set column alignment, or you can manually set the alignment using a `:` to at the beginning or end of the header to indicated explicit direction:

* `:Left Aligned`
* `Right Aligned:`
* `:Center Aligned:`

These options are also available via the **Context Menu -> Align  Column**, which then sets these Markdown hints on the header.

### Preview while you Edit
Although the Table Editor uses the current preview theme while editing, the edit document doesn't look very close to the actual output - especially if you also include embedded Markdown formatting in your tables. If you want to see the actual rendered table **as you move out of each colunmn** you can use the preview option on the toolbar to activate the preview pane:

![](/images/TableEditorPreview.png)

### Keyboard Shortcuts
A number of Keyboard shortcuts make common operations easy without moving your hands off the keyboard:

+----------------------+---------------------------------------------------------------------------+
| Shortcut Key         | Operation                                                                 |
+======================+===========================================================================+
| **Tab**              | Move to next field or - If tabbing past last item, a new row is added.    |
+----------------------+---------------------------------------------------------------------------+
| **Arrow Keys**, \    | Navigate table cells.                                                     |
| **Ctrl-Arrows**      |                                                                           |
|                      | In multiline text fields the arrow keys behave as editor navigation keys. |
|                      | You can use *ctrl-arrow* to navigate.                                     |
+----------------------+---------------------------------------------------------------------------+
| **Alt-Shift-Down**,\ | Insert new row below or above.                                            |
| **Alt-Shift-up**     |                                                                           |
+----------------------+---------------------------------------------------------------------------+
| **Alt-Shift-Del**    | Delete current row.                                                       |
+----------------------+---------------------------------------------------------------------------+
| **Alt-Up**\          | Move row up or down                                                       |
| **Alt-Down**         |                                                                           |
+----------------------+---------------------------------------------------------------------------+
| **Alt-Left**\        | Move column left or right                                                 |
| **Alt-Right**        |                                                                           |
+----------------------+---------------------------------------------------------------------------+