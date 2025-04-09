Markdown Monster's configuration settings are stored in a simple JSON file. The default location of the configuration file is:

`%appdata%\Markdown Monster\MarkdownMonster.json`

and the file is simply editable either directly, or by using **Tools -> Settings**.

By using a shared location you can easily share all configuration settings across multiple machines. All settings are shared including:

* Editor Styling
* Font choices
* Recent and Open Documents
* Window locations (MM auto adjusts if locations don't fit)
* many more

Because settings include personal options like which files are open and recent, these settings are considered **per user**.

### Changing Configuration Folder to DropBox or OneDrive
The best way to share configuration settings is to use a shared cloud drive like DropBox, OneDrive or Google Drive.

You can change the location of the configuration folder using the **CommonFolder** setting in the Markdown Monster Settings at **Tools -> Settings**. 

For example, you can easily set the CommonFolder to a shared location on a cloud drive like Dropbox:

```json
CommonFolder="C:\\Users\\rick\\Dropbox\\Markdown Monster Common"
```

Save the file and exit Markdown Monster.

> #### @icon-info-circle Make sure the Folder Exists
> When setting a shared configuration location for the first time, make s
sure the custom folder you configure exists by copying the old folder to the new location.
>
> The configuration folder holds all configuration settings as well as all addins that are installed, so the entire configuration can be shared.
>
> Each subsequent installation of Markdown Monster that wants to then share the common location only has to change the `CommonFolder` configuration settings.

### How it works
Markdown Monster relies heavily on the `MarkdownMonster.json` configuration settings which are read when Markdown Monster starts. 

However, when you redirect the file, the file does not live in its *usual* location, so another file is needed to redirect it to the actual location. If the location is non-default there should be a file named:

```txt
%appdata%\Markdown Monster\CommonFolderLocation.txt
```

which contains a single string with the location of the actual Common folder path. 

> `%appdata%` is an environment variable, so if you're running a virtual environment (like Wine on Linux) you can set an `appdata` environment var to some known location in that environment and then put configuration data there. Make sure the folder has **read/write** access.

If the `CommonFolder` setting is different than the default `%appdata%` location, MM writes a special file  `%appdata%\Markdown Monster\CommonFolderLocation.txt` to find the custom location of the configuration file. If this file exists when loading the configuration, MM tries to read the file from the new location and if it's found then uses the configuration settings from this location. If the file is not found, MM reverts back to the default location.