Markdown Monster ships both as a **full installer**, and a **portable install** that is delivered as a Zip archive. Both versions also come as Chocolatey packages.

* **Full Installer**  
The full installation requires elevated rights for registering several system components.

* **Portable Installation**  
The Portable Zip file contains all the files to run Markdown Monster, and you can simply copy those files into any folder on your local machine - there is no installation required and you don't need Administrator rights to get started.

> #### Portable Version requires a Writable Location for Settings
> The portable version can run out of any folder, but for a fully self contained install that includes both the binaries and the application's stored settings that are updated as you run, you have to choose a **writable location**, or at minimum make the configuration folder writable. You can install to a USB drive, or `My Documents` or `Local AppData` which have permissions for your app to write files.
>  
> Alternately you can run from any location - including a non-writable one - in shared mode which creates the settings folder in its default location in `%appdata%\Markdown Monster` where it can safely write files. Shared mode kicks in automatically if settings and registration cannot be written to the portable configuration folder in the install folder.

You can download and install the portable version from here:

* [Markdown Monster Portable Install](https://markdownmonster.west-wind.com/download)

It's also on Chocolatey

```ps
choco install MarkdownMonster.Portable
```

The portable zip file is the easiest way to get a portable install but you can also copy any installed version of Markdown Monster from the `%localappdata%\Markdown Monster` folder and simply put it on a USB drive or other portable device that you want to run Markdown Monster from.

By default however, Markdown Monster does not run in local settings mode, but puts settings into `%appdata%\Markdown Monster`. This can be overridden with a setting however, so it's stored in the application folder.

### Enabling and disabling Portable Mode 
The first time Markdown Monster starts it looks for configuration data and if it doesn't find it, it creates it. By default, in non-portable mode the configuration location is the `%appdata%\Markdown Monster` folder, but when portable mode is enabled a local `.\PortableSettings` folder in the install directory is used instead. If that folder cannot be created, configuration falls back to writing to the shared `%appdata%` location.

Portable mode is determined by a special file in the Markdown Monster installation folder:

`_IsPortable`

The portable zip install includes this file so when you start the application it'll automatically pick up this file and run in portable mode. 

You can also manually add this file to an existing installation of Markdown Monster and force it to switch to portable mode or use the `-setportable` command line switch.

### Settings Storage
The key difference between `portable` and `installed` modes at runtime is where configuration data is stored:

**Portable Mode**  
`<installFolder>\PortableSettings`

**Normal Mode**  
`%appdata%\Markdown Monster`

### Command Line Switches to Turn Portable Mode on and Off
You can also toggle Portable mode on and off using command line switches:

**Turn on portable mode:**

```ps
mmcli -setportable
```

**Turn off portable mode:**

```ps
mmcli -unsetportable
```

### Configuration Folder
The configuration folder holds the main Markdown Monster `MarkdownMonster.json` configuration file, as well as any downloadable addins that you might install. In addition, third party addins also tend to use this folder to store their configuration information.

> ### @icon-warning Portable Folder Permissions
> In order to run a local portable install, make sure that you run a portable install out of folder that has **read/write access** for the `.\PortableSettings` folder. By default MM runs out of %applocaldata% which has read/write access but if you choose a portable folder make sure write permissions are available or settings cannot be saved in the `.\PortabeSettings` folder and will revert to save into `%appdata%\Markdown Monster`.


### Running with Missing Permissions
If you don't use a folder with the appropriate permissions Markdown Monster still works, but several things can happen:

* Configuration settings will be written to a machine specific location in `%appdata%\Markdown Monster` which is not portable.
* Addins may fail to load if Execute or AV permissions don't allow for executable code.

If you installed into a restricted folder and don't want to move the installation, you can also add the required permissions. You can give `Read/Write/Execute` permissions to the `.\PortableSettings` folder to your user account or the `Interactive` account to allow the local folder to be used.

### Uninstall Persisted Configuration Settings
Markdown Monster requires a few user settings in the registry in order to work correctly. When installing the portable install these settings are written the first time MM starts up.

Specifically it adds:

* Markdown file association for MM
* Internet Explorer compatibility mode for MM
* MM adds itself to the User's path environment var
* An instance key for the application

These settings are checked on startup of the application and created if not already present.

Since there's no uninstaller when you use the portable version, you can manually remove these registry settings by running the following from the command line:

```text
mmcli -uninstall
```

Make sure you run this command after Markdown Monster has shut down, otherwise some of these values may get re-written when MM exits (or restarts).

### Chocolatey's Portable Install - Non Admin but not Portable
Markdown Monster includes a portable install from Chocolatey that you can install with:

```text
choco install MarkdownMonster.Portable
```

Although this install says it's portable due to Chocolatey Naming conventions, it actually does not install in a truly portable way. It allows for non-Administrator installation but it uses the machine specific `%appdata%\Markdown Monster` location for storing settings by default.

The portable installation is created in:

```
c:\ProgramFiles\Chocolatey\lib\MarkdownMonster.Portable\Tools
```

which **does not allow for write access** for an unelevated account which results in use of the  `%appdata%\Markdown Monster` folder for settings. If you want local data that is portable you can explicit create the `.\PortableSettings` folder and give it full rights to your user account.

Use the Chocolatey Portable package for the non-admin install feature, but use the [standalone portable installer](https://markdownmonster.west-wind.com/download) if you want a truly self-contained, portable installation in a location of your choice.