Markdown Monster's editor is based on <a href="https://ace.c9.io/#nav=about" target="top">ACE Editor</a> and inherits the core editing features from this awesome HTML based editor. ACE provides the basic editor behavior you'd expect for a full featured text editor, and Markdown Monster adds a few additional application specific keyboard shortcuts on top of that base behavior.

### ACE Editor Keys
You can find a list of core ACE editor features here:

* <a href="https://github.com/ajaxorg/ace/wiki/default-keyboard-shortcuts" target="top">Ace Editor Keyboard shortcuts</a>



### Markdown Monster Application Shortcuts
Markdown Monster adds a number of additional hotkeys to access common functionality more easily. You can discover most of these hotkeys on the menus, or on the tooltips of the toolbar.

<table class="detailtable" style="width: 96%;margin-top: 20px">
<tr>
    <th colspan="2">
        Preview Browser Operations
    </th>
</tr>
<tr>
  <td>Ctrl-Shift</td>
  <td>Refresh the preview browser immediately if active</td>
</tr>
<tr>
  <td>Ctrl-Shift up/down</td>
  <td>Scroll the preview browser</td>
</tr>
<tr>
  <td>Alt-V-P</td>
  <td>Toggle the preview browser</td>
</tr>
<tr>
  <td>Alt-V-B</td>
  <td>Preview html in external browser</td>
</tr>
<tr>
    <th colspan="2">
        File and Export Operations
    </th>
</tr>
<tr>
  <td>Ctrl-N</td>
  <td>Create new untitled document</td>
</tr>
<tr>
  <td>Ctrl-O</td>
  <td>Open a document from disk</td>
</tr>
<tr>
  <td>Ctrl-S</td>
  <td>Save active document</td>
</tr>
<tr>
  <td>Ctrl-Shift-S</td>
  <td>Save active document with new name</td>
</tr>
<tr>
    <th colspan="2">
        Markdown Conversion
    </th>
</tr>
<tr>
  <td>Ctrl-Shift-C</td>
  <td>Copy selected Markdown text as HTML to Clipboard</td>
</tr>
<tr>
  <td>Ctrl-Shift-V</td>
  <td>Paste HTML from Clipboard as Markdown text</td>
</tr>
<tr>
  <td>Ctrl-Shift-Z</td>
  <td>Remove Markdown Formatting</td>
</tr>
<tr>
    <th colspan="2">
        Editor Operations
    </th>
</tr>
<tr>
  <td>Ctrl-B</td>
  <td>Bold selected text</td>
</tr>
<tr>
  <td>Ctrl-I</td>
  <td>Italicize selected text</td>
</tr>
<tr>
  <td>Ctrl-L</td>
  <td>Create List from multiple lines of text</td>
</tr>
<tr>
  <td>Ctrl-Q</td>
  <td>Quote selected text</td>
</tr>
<tr>
  <td>Ctrl-K</td>
  <td>Insert or create link from selected text (dialog)</td>
</tr>
<tr>
  <td>Ctrl-Shift-K</td>
  <td>Insert or create link inline (text only)</td>
</tr>
<tr>
  <td>Ctrl-J</td>
  <td>Insert Emojii from Picker</td>
</tr>
<tr>
  <td>Alt-C</td>
  <td>Format selected text as code block</td>
</tr>
<tr>
  <td>Ctrl-`</td>
  <td>Format selected text as inline code</td>
</tr>
<tr>
  <td>Alt-X</td>
  <td>Show Extended Markdown Operations Dropdown Menu</td>
</tr>
<tr>
    <th colspan="2">
        Find
    </th>
</tr>
<tr>
  <td>Ctrl-F</td>
  <td>Find in document</td>
</tr>
<tr>
  <td>F3</td>
  <td>Find Next</td>
</tr>
<tr>
  <td>Ctrl-Shift-F</td>
  <td>Find in Files</td>
</tr>
<tr>
    <th colspan="2">
        Other
    </th>
</tr>
<tr>
  <td>F7</td>
  <td>Next Spellcheck Error</td>
</tr>
<tr>
  <td>Shift-F7</td>
  <td>Previous Spellcheck Error</td>
</tr>

<tr>
    <th colspan="2">
        Toggles
    </th>
</tr>
<tr>
  <td>Alt-V-W</td>
  <td>Toggle Word Wrap</td>
</tr>
<tr>
  <td>Alt-V-N</td>
  <td>Toggle Line Numbers</td>
</tr>
<tr>
  <td>Alt-V-B</td>
  <td>Toggle the Preview Browser</td>
</tr>
<tr>
<tr>
    <th colspan="2">
        Text Selection and Navigation
    </th>
</tr>
<tr>
  <td>Ctrl-Shift-Arrow</td>
  <td>Select word left and right</td>
</tr>
<tr>
  <td>Ctrl-Shift-Home/End</td>
  <td>Select to beginning or end of line</td>
</tr>
<tr>
  <td>Ctrl-Shift-D</td>
  <td>Duplicate selection and paste after</td>
</tr>

<tr>
  <td>Alt-Drag up and down</td>
  <td>Block Selection across multiple line</td>
</tr>
<tr>
  <td>Ctrl-Alt-Up/Down</td>
  <td>Create multiple cursors for simultaneous input</td>
</tr>


<tr>
    <th colspan="2">
        Editor Admin
    </th>
</tr>
<tr>
  <td>Ctrl-,</td>
  <td>Brings up Ace Editor Settings menu</td>
</tr>
</table>


### Multi Select Text
ACE support multi-selection of text by using `Ctrl-Select`. Hold down the `Ctrl` key make a selection then let up. With the selection still active press `Ctrl` again and select another area of text. Both selections are now active. Repeat for additional selections.

With multiple selections active you can now type and change text in all selected areas.

### Block Selections (multi-line)
You can also select vertical blocks in Ace Editor. To use Block Selection hold down the `Ctrl` key and drag a rectangle to make a selection of the text in the rectangle area.

With the selection active, when you type the text on each row is changed.