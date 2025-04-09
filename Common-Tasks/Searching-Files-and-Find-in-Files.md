There are several ways that you can search and filter files in the Folder Browser. You can search for files by name, and also use a content search with **Find in Files**.

The following Folder Browser search mechanisms are available:

* Inline Explorer-like Filename Search (type to jump to file)
* Find File by name search box (Ctrl-F)
* Find in Files to search file content (and also file names) (Ctrl-Shift-F)

![Find in Folder Browser](https://github.com/RickStrahl/ImageDrop/raw/master/MarkdownMonster/FindAndFindInFiles.gif)


### Explorer Style Filename Search
You can type a partial file name when inside of the folder browser list and the selection will jump to the first file that matches what you typed.

![](/images/FolderBrowser_FilenameSearch.png)

This behavior is similar to the way Windows Explorer finds files in the currently active folder.

> The Explorer style search only searches the current level of the tree - it doesn't search into sub folders. For that you can use the File Search Box.

This is a very simplistic search useful while navigating files.

### File Search Box
You can use `Ctrl-F` in the file browser to jump to the File Search Box at the top of the folder browser. This search looks file names that that contain the search text.

The search is incremental  and results show as a filtered tree list as you type:

![](/images/SearchFiles.png)

To avoid potentially very slow searches the search box defaults to searching only the active folder. Toggle the folder button to the side of the search box to also search sub folders. Be aware if you have a deep folder structure this can be slow.

Make sure to clear the Search Text to get back to the full file list.

### Find in Files
You can use `Ctrl-Shift-F` in the Folder Browser to find content in files:

![](/images/FolderBrowser_FindInFiles.png)

There are a number of options in this small form:

* Search Subfolders
* Search Content
* Specify file extensions
* Specify the search folder
* Specify a replace expression for matches

By default the search folder is the active folder in the folder browser, but you can change the folder to a different location.

By default search sub-folders and search content are enabled so the default search is effectively a *Find in Files* search. By turning off the search in content option you can speed up the search if you're only looking for files by name in the folder hierarchy.

When you click on a selection the editor is opened and the search text is pushed into the Search Box. If you set the Replace text that text is set in the Replace box of the editor search box.