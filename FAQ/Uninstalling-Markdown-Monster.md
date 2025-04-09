Markdown Monster is a pretty light installation and can be installed as a local folder (portable) install that can simply be xcopied to a new location and run. However MM sets a couple of user wide settings that are not cleaned up **if you simply removed the Markdown Monster installation folder**. 

Markdown Monster sets the following user wide settings (in the registry):

* Adds Markdown Monster to the User path
* Adds several Markdown related file associations
* Adds Browser Emulation to the registry

### Full Version Uninstaller
If **you installed Markdown Monster using a full installation** with the full installer or non-portable Chocolatey package, you can simply use the **Markdown Monster Uninstaller** in the Windows **Programs and Features** applet which removes all system settings.

Uninstall won't remove the User Settings folder (see below).

### Uninstalling a Portable Install
You can remove the above mentioned user settings from a portable istall by running the following command from the Windows Command Prompt:

```
mm -uninstall
```

> #### @icon-info-circle Settings are Reinstalled on full Launch
> Markdown Monster creates the above settings when it launches so if you remove them using `mm -uninstall` make sure you don't restart MM as the settings are simply re-created. 

Uninstall generally only makes sense if you are done with Markdown Monster and want to completely remove it from your system.

### Removing the User Settings Folder
The user settings folder is stored in:

```
%appdata%\Markdown Monster
```

This folder holds the Markdown Monster configuration file, as well as any addins and addin settings that you might have installed.

Markdown Monster does not delete this folder during either full or portable uninstallation since it contains user modified data.

If you don't plan on coming back to Markdown Monster you can safely **delete this folder explicitly**.

### Removing the Markdown Monster Install Folder
A full install of Markdown Monster installs into this location:

```
%LocalAppData%\Markdown Monster
```

The full uninstaller will remove all installed files, but may leave behind  small uninstaller marker files after an uninstall in some situations. After uninstall you can **safely remove this folder**.