The **Tab context menu** and also the **Tools menu** provides a number of useful options for working in the active document's folder and accessing the theme and configuration folders.

Here's what the tab context menu looks like:

![](/images/TabContextMenu.png)

And here's what the Tools Menu looks like:

![](/images/toolsmenu.png)

Here's what all the options do:

##### Open Folder
Opens the active document's folder in Windows Explorer. This makes it easy to see and edit related documents like images or make changes to filenames etc.

##### Open Terminal
Opens a Windows Command Prompt in the active document's folder. This can be useful if you need to do a Git Commit on documentation files or a blog post hosted through Git for example. 

##### Commit and Push To Git
Click this menu option to commit the active document to Git and then push it to the configured Git origin. Assumes that Git is available globally (git.exe) and that the Git is already configured for the document's containing folder.

##### Open Configuration Folder
This opens the Markdown Monster global configuration folder where you find configuration files for Markdown Monster and most addins. The main configuration is `MarkdownMonster.json` which contains the same configuration setting you can set with the **Settings** menu option. You also have access to `WeblogAddin.json`, and `ScreenCaptureAddin.json` their respective configuration settings. Third party addins also tend to store their JSON configuration files in this folder.

###### Open Preview Themes Folder
This opens the Preview Themes folder, where preview themes are defined. Preview themes consist of a folder that has a `Theme.html` and `Theme.css` files.

![](/images/PreviewThemeFolder2.png)

To create a new theme simply copy one of the existing themes and modify the files - most likely only the `theme.css` file. Any new folders you create will show up in the Preview Theme list next time you restart Markdown Monster.

##### Settings
This opens the `MarkdownMonsterSettings.json` file in Markdown Monster. You can make changes to this document and the changes are applied as soon as you save the document.