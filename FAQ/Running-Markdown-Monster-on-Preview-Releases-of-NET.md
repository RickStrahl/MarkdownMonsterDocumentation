Markdown Monster can run with the latest .NET Release and automatically rolls forward to the latest .NET Core release of the .NET Windows Desktop Runtime installed on the machine. 

So even if Markdown Monster is compiled for .NET 6.0 it can run on .NET 7.0.

It's also possible to run Markdown Monster on Preview releases of .NET Core. Currently the release version of .NET is 7.0.11 and there's an RC for .NET 8.0 available. Even if you have the .NET 8.0 Windows Desktop Preview Runtime installed, MM won't automatically use that version because it's a preview release.

If you would like to use a preview release you'll need two things:

* **.NET Windows Desktop Runtime**  
<small>*(here's the [.NET 8.0 RC](https://dotnet.microsoft.com/en-us/download/dotnet/8.0) download page)*</small>
* Set `DOTNET_ROLL_FORWARD_TO_PRERELEASE` Environment Variable

## Set the Environment Variable
You can use the following to set the environment variable:

**Setting from the Terminal (Powershell)**

```powershell
# In session Environment variable
$env:DOTNET_ROLL_FORWARD_TO_PRERELEASE=1
# Launch Markdown Monster
MarkdownMonster 
```

or - the easier way - via a global environment setting in your User or System Environment:

![](/images/PreviewRollForwardEnvironmentVariable.png)

Once you set the user or system environment you'll have to restart Explorer or whatever shell you are using to launch Markdown Monster from to see the change.

Once you've done this Markdown Monster can now use the latest preview release.

![](/images/LatestPreviewReleaseofDotnet.png)