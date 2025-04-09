Markdown Monster uses [ACE Editor](https://ace.c9.io) for its editor, which is an HTML based editor implementation. There are a few things that can be customized in the editor including things like the cursor formatting, search box formatting and some basic text input features.

You can take a look at `editor.css` in the `Editor` folder of the installation to see some of the customizations that MM does to the stock editor.

If you want to customize any of these settings, you should override them by creating a new file called `editor-user.css`. This file is a user file that **won't be overwritten by Markdown Monster updates** unlike changes that are made directly in `editor.css`.

### Example: Change Cursor Width
For example to change the cursor width in the editor:

Create a new file `Editors\editor-user.css`.

Then add any custom styling in this CSS file. For the cursor width:
```css
.ace_cursor { 
    border-left: 4px solid !important;
}
```