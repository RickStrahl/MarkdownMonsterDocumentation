If for some reason Markdown Monster gets out of whack and you have problems starting the application or you have other issues that might be caused by a corrupt configuration, you can reset Markdown Monster to its install settings.

You can do this by running:

```
mm reset
```

from a Windows Command prompt or Powershell **after you have shut down Markdown Monster**.

### What it does
The reset operation deletes the old `%appdata\Markdown Monster\markdownmonster.json` configuration file, resets all the settings to default and then writes out a new configuration file. 

Markdown Monster also creates a backup file of your old configuration for reference with a `-reset-xx-xx-xxxx.json` extension.

Reset also removes the `Addins` folder in the same location which effectively removes all addins that were installed.

> ### @icon-info-circle Specific Addin Settings are not removed
> Markdown Monster **does not** remove addin configuration settings which are typically stored in the same `%appdata%\Markdown Monster\` folder, so when you reinstall addins any settings for those addins are still available. If you want to reset addin settings rename or delete the addin specific `.json` files.