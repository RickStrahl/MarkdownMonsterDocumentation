Markdown Monster has a limited support for previewing DocFx Markdown which uses the following syntax:

```txt
[!include[title](relativeFilename)]
```

Markdown Monster pre-processes the Markdown document for these links and if found attempts to resolve any relative file link by first checking to see if the file exists and if so pulling the content into the current markdown document.

> ##### @icon-info-circle No YAML Support for Included Files
> included files may not include YAML content. If they do, the YAML is rendered.

Here are some examples of what can be included:

##### Relative Paths
```
[!include[displays file](fileToInclude.md)]
[!include[displays file](sub/fileToInclude.md)]
[!include[displays file](../lowerSub/fileToInclude.md)]
```

##### Root paths scoped to Folder Browser
```
[!include[displays file](~/lowerSub/fileToInclude.md)]
```

Note the last item which uses `~` virtual root character which points the 'site' root. Since on the desktop there is not 'site', the site root path is based on the path that is open in the [Folder Browser](VFPS://Topic/_4WU1CJYKA).



