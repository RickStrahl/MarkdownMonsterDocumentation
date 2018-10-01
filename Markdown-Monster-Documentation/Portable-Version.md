Markdown Monster ships both as a fully installed installer package and a portable version that simply is a Zip archive that contains all the source files.

You can get the portable version from here:

* [Markdown Monster Portable Install](https://markdownmonster.west-wind.com/download.aspx)

The portable version can run out of any folder but preferably choose a writable location.

The portable zip is the easiest way to get a portable install but you can also copy any installed version of Markdown Monster from the `%appdata%\Markdown Monster` folder and simply put it on a USB drive or other portable device that you want to run Markdown Monster from.

### Enabling and disabling Portable Mode 
Portable mode is determined by a special file in the Markdown Monster installation folder:

`_IsPortable`

The portable zip install includes this file so when you start the application it'll automatically pick up this file and run in portable mode. 

You can also manually add this file to an existing installation of Markdown Monster and force it to swich to portable mode.

### Settings Storage
The key difference between `portable` and `normal` modes at runtime is where configuration data is stored:

**Portable Mode**  
`<installFolder>\PortableSettings`

**Normal Mode**  
`%appdata%\MarkdownMonster`

These folders hold the main Markdown Monster `MarkdownMonster.json` configuration file, as well as any downloadable addins that you might install. In addition, third party addins also tend to use this folder to store their configuration information.

> ### @icon-warning Portable Folder Permissions
> In order to run a local portable install, make sure that you run a portable install out of folder that has read/write access for the `.\PortableSettings` folder. By default MM runs out of %applocaldata% which has read/write access but if you choose a portable folder make sure write permissions are available or settings cannot be saved at runtime.

### Command Line Switches to Turn Portable Mode on and Off
You can toggle Portable mode on and off using command line switches:

**Turn on portable mode:**

```ps
.\MarkdownMonster -setportable
```

**Turn off portable mode:**

```ps
.\MarkdownMonster -unsetportable
```

### Persisted Configuration Settings
Markdown Monster requires a few user settings in the registry in order to work correctly. Specifically it adds:

* Markdown file association for MM
* Internet Explorer compatibility mode for MM
* MM adds itself to the User's path environment var
* An instance key for the application

These settings are checked on startup of the application and created if not already present.

If you decide you want to completely remove Markdown Monster and clean up you can remove these settings with a command line switch:

```
markdownmonster -uninstall
```

Make sure you run this command once MM is shutdown otherwise some of these values get re-written on subsequent startup.
