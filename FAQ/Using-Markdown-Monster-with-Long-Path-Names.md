Markdown Monster has limited support for Long Path names, but it requires some Windows configuration to enable this functionality.

Windows by default does not support path names over 260 characters (`MAX_PATH`) using the standard Windows file access APIs. This means that if you try to open or save files that have paths (folder + file name) that exceed 260 characters those files can fail to open in Markdown Monster.

## Override Windows Settings for Long Path Support
Markdown Monster has support for long file names, **but it only works if the Windows operating system has been enabled for Long Paths** which is done via a registry or group policy setting.

This setting essentially enables Long Path support for applications that request it, using standard Windows APIs without changes. Unfortunately this is not a default setting in Windows, so it has to be manually enabled and each application has to explicitly support it. Markdown Monster does, although there are some limitations.

Let's look at how to enable Long Path support in Windows.

### Using mmCli
The easiest way to enable long paths on Windows is to the use the Markdown Monster `mmCli` command. This command is globally registered via your path, so you should be able to run it from anywhere.

You can use the following commands from the Markdown Monster CLI to toggle the Long Path support in Windows

```ps
# Turn on long paths
mmcli enable-windows-longpaths

# Turn them off
mmcli disable-windows-longpaths
```

### Using the Registry
If you'd rather know what's going on you can use the registry directly either via the Registry editor, `.reg` script or a Powershell command. 

You can save and run the following save the following text to a  `.reg` file and execute it from Explorer or the Command Line. Copy to a .reg file or manually set this registry key running as Administrator:

```text
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\FileSystem]
"LongPathsEnabled"=dword:00000001
```

or you can use Powershell from an Administrative Terminal:

```ps
Set-ItemProperty `
  -Path HKLM:\SYSTEM\CurrentControlSet\Control\FileSystem `
  -Name LongPathsEnabled -Value 1
``` 

### Using Group Policy
You can also enable this functionality via Windows Group Policy, by setting:

![](/images/LongFilenameGroupPolicyEnabling.png)


### It Works - mostly
Once you've set one of these options restart Markdown Monster and you should now be able to open and save files that exceed 260 character paths. This applies to all file operations that open files into the editor and save files like images, PDF or HTML files etc.

## Caveats: Not everything works!
Although this setting allows you to open and save documents and related assets using long paths, **other applications and related support tools and components may not work correctly with long file names**. Even Windows components like Windows Explorer and Powershell have issues with long file name support, so be weary. In Markdown Monster this may mean shelling out to folders or files with long paths may not work as the external applications might not work with the long paths.

In short, Markdown Monster's key features related to file operations work fine. But there are some failures, or missing features with external support tools.

### Chromium Preview and Relative Resource Links
Maybe the most pressing issue related to Long Path file usage is is that if you have a document with a long filename and related resources like images that are referenced as *relatively pathed items* (ie. `![](./myimage.png`), the Chromium previewer *(or any Chromium based browser for that matter)* will not render the relative path if the host page is a long filename, as the browser fails resolve the long path for the relative link. 

In Markdown Monster this impacts the previewer with potentially missing images, as well as image previews in the Folder Browser, Image Linking and Capture windows etc. 

> #### @icon-warning Recommendation: Don't use Long Paths if you can avoid it
> While the settings described here make MM work with long paths, to avoid the side effects described above and also other OS related issues, it may be best to minimize or avoid paths that exceed the 260 character limit.

> ####  @icon-info-circle Long Path Alternatives
> 260 character paths **allow for very long paths** without going over the limit. If you really, really need to dig into deeply nested hierarchies, consider breaking up your folder hierarchies to be shorter, shortening names or using symbolic links or folder mapping to shorten base paths to avoid excessive path lengths.