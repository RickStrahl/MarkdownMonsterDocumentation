Markdown Monster can detect file changes for the underlying files of open documents in the editor and show those changes. Depending on whether the active document has pending changes, the editor can immediately show the file updates, or - if there are pending changes - prompt for a file comparison when saving the document.

![](https://github.com/RickStrahl/ImageDrop/raw/master/MarkdownMonster/FileChangeDetection.gif)

### Open Editor has no Pending Changes
If the open document **has no changes**, the file is immediately updated with the changes.

### Open Editor has Pending Changes
If the open document **has changes**, nothing immediately happens until you **save the file**. 

When you save the document you get the option to

* **Use Yours** - immediately writes your current text to file.   
* **Use Theirs** - loads the file from disk into the editor.  
* **Compare** - brings up your configured Diff tool and you can save the file from there. If you save the right or left file (in that order) - that file will be used to re-load the editor which allows for you to merge your changes.    
***Note**: You have to save the document in the Diff tool to apply any changes, otherwise the document remains unchanged*
* **Cancel** - doesn't save right now.