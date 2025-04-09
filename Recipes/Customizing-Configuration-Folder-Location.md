Markdown Monster's configuration settings are stored in a simple JSON file. The default location of the configuration file is:

`%appdata%\Markdown Monster\MarkdownMonster.json`

and the file is simply editable either directly, or by using **Tools -> Settings**.

### Changing Configuration Folder to DropBox or OneDrive
You can also change the location configuration of the configuration folder using the **CommonFolder** setting in the Markdown Monster Settings at **Tools -> Settings**. 

For example, you can easily set the folder to a shared location like Dropbox:

`CommonFolder="C:\\Users\\rick\\Dropbox\\Markdown Monster Common"`

> Make sure the custom folder you configure exists. Markdown Monster will not create it and if it doesn't exist, reverts back to the default location. We recommend that you create the folder and copy the contents of your existing configuration folder to the new location explicitly.

Note that changing this setting affects all configuration settings including settings for addins and other components. 

So if you change the folder make sure you first copy your existing `%appdata%` settings over to the shared location - otherwise a new set of settings will be created.

Once on a shared drive, configuration settings can now be accessed from any Markdown Monster instance that also is connected to this shared drive.

> #### Figuring out the Configuration Location
> Markdown Monster uses another file - `%appdata%\Markdown Monster\CommonFolderLocation.txt` - if a custom location has been specified to hold this location. If this file exists Markdown Monster looks at it for the new location for configuration. This file is created whenever the configuration file is saved from within Markdown Monster and if the folder differs from the default location.