To facilitate creation of Add-ins Markdown Monster provides an installable addin template that can be used from either the command line via **dotnet new** or from **Visual Studio New Project Dialog**.

To install the template, use the following from the Windows Command Prompt:

```ps
dotnet new install MarkdownMonster.AddinProject.Template
```

**Prerequisites:**
* [.NET SDK](https://dotnet.microsoft.com/download/) (v8.0 or later)  
The free .NET SDK is required to build the Addin project. It includes the C#/.NET compiler and build tools to create the addin binary. You can use any editor to build your .NET code and then use `dotnet build` to create the addin. If you're using Visual Studio, the .NET SDK is automatically available and used behind the scenes.

* [.NET Desktop Runtime](https://dotnet.microsoft.com/download/) (should be installed with Markdown Monster)  
Markdown Monster is a Windows Desktop application so it needs the .NET Core Runtimes. If you're building this addin on the same machine as MM, the runtime should be installed already.

## What does the Project Template do?
The addin template creates a ready-to-run starter Addin project for you that does the following:

* Creates an SDK style .NET 8.0 Class Library Project  
  *Make sure the project name (specifically the result assembly) ends `Addin` (as in `MyGreatAddin`)*
* Creates a class that inherits from `MarkdownMonsterAddin`  
* Implements `OnApplicationInitialized()` to configure the Addin
* Stubs out a few common event handlers for MM life-time event handling
* Includes a dummy button handler that tests initial Addin installation
* Includes a `build.ps1` script to package your addin

Once the base is installed you can then:

* Implement the `OnExecute()` and `OnExecuteConfiguration()` handlers
* Optionally you can hook into many other addin events
* Compile project output into `%appdata%\Markdown Monster\addins\YourAddin`
* *Note:* Make sure your project assembly (or project name) ends in `Addin.dll` (ie. `MyKillerAddin.dll`)

You can create a new Markdown Monster addin project in one of two ways:

* Using `dotnet new`
* Using Visual Studio

Let's go through these steps in detail.

## @icon-download Create an Addin with the *dotnet new* Template
The `dotnet new` template is an installable template that can be used with the `dotnet new` command and also in Visual Studio. You can install the Nuget package after which you can then use the template to create a new Markdown Monster Addin project. By default this is done **from the command line** although you can also run the template from the Visual Studio New Project dialog once the template is initially installed.

To use the `dotnet new` template is a two step process:

* Install the Markdown Monster Addin Template from NuGet
* Create the Addin Project

The template is available [via NuGet](https://www.nuget.org/packages/MarkdownMonster.AddinProject.Template/) and you can install it using `dotnet new install` CLI SDK tooling. You need to have a recent [.NET Core SDK](https://dotnet.microsoft.com/download/) installed in order to run `dotnet new`.

To install the template you'll use the `dotnet new install` CLI command from the Terminal:

```ps
dotnet new install MarkdownMonster.AddinProject.Template
```

You can then create a new project like this:

```ps
# Create a folder for your project and change to it
md \projects\SampleAddin
cd \projects\SampleAddin

# Create the new Project - make sure the name ends in 'Addin'
dotnet new markdownmonsteraddin -n SampleAddin --company "West Wind Technologies"

# Build the project - should create a placeholder addin
dotnet build 

# Start Markdown Monster - placeholder Addin should be loaded (bullhorn icon on toolbar)
mm
```

> ##### @icon-warning Custom Install Locations
> To run as-is as shown above assumes that Markdown Monster is installed in its default `%ProgramFiles%\Markdown Monster` location. If MM is installed in a different location, you'll need to replace the `$(ProgramFiles)` binary location, and `$(AppData)` configuration folder location references in the `.csproj` file to point at your custom locations.

At this point Markdown Monster should show a Bullhorn icon in the toolbar for the new Addin you've created. You can click on the icon and it should display a message box with a template message. If you see this behavior you're all set to add your custom functionality and replace the default behavior.

You can then open the project in your .NET IDE of choice by clicking on the `.csproj` file.

## @icon-download Create an Addin Project with the Visual Studio Extension

> The `dotnet new` installed template can also be accessed in Visual Studio 2022+ via the  **New Project Dialog**.

Start by creating a new project by searching for **Markdown Monster** in the search box. Select  **Markdown Monster Addin Project** and follow the prompts to create a new project. Make sure the name ends in `Addin`. I'll use one called **SampleAddin**:

![](/images/CreateAddinProject.png)

The project type created is a .NET 8.0 Class Library. Next specify the project name.

> **Important:** Make sure the **project name ends in `Addin`** (ie. `SampleAddin` or `RefactoringAddin`). The addin manager looks for files that end in `Admin.dll` to ensure your addin is found in the common `Addins` folder.

![](/images/CreateAddinProject2.png)

Once installed you can run the project to compile and build into the Addins folder. You should also be able to debug the application with the default settings.

> ##### @icon-warning Custom Install Locations
> To run as-is as shown above assumes that Markdown Monster is installed in its default `%ProgramFiles%\Markdown Monster` location. If MM is installed in a different location, you'll need to replace the `$(ProgramFiles)` binary location, and `$(AppData)` configuration folder location references in the `.csproj` file to point at your custom locations.

## What's created by the Project Templates and customizing the Project
Both the CLI and Visual Studio templates create the same output. 

The project is created as a .NET Core Class Library project, which builds its output into the Markdown Monster common `Addins` folder (by default `%appdata\Markdown Monster\Addins`), which is where Markdown Monster looks for custom addins to load. If you want to use Visual Studio or another IDE with the CLI generated project, simply open the `SampleAddin.csproj` file in your IDE and you're good to go.

The project should be ready to build, compile and let you run in the debugger in Visual Studio. From the command line use `dotnet build` and then run `mm` to launch Markdown Monster which then loads the addin.

For reference or if you want to manually create your project without the template, here's what the generated project file looks like:

```xml
<Project Sdk="Microsoft.NET.Sdk">
	<PropertyGroup>
		<Version>0.1</Version>
		<TargetFramework>net8.0-windows</TargetFramework>
		<UseWPF>true</UseWPF>

        <!-- If you use a custom common data folder (or portable install) explicitly provide the path here -->
		<OutDir>$(appdata)\Markdown Monster\Addins\SampleAddin</OutDir>

		<DebugType>embedded</DebugType>
		<DebugSymbols>true</DebugSymbols>
	</PropertyGroup>

	<ItemGroup>
	    <!-- point at Markdown Monster startup folder if you installed in a custom location --> 
		<Reference Include="$(ProgramFiles)\Markdown Monster\MarkdownMonster.dll">
			<Private>false</Private>
			<IncludeAssets>compile</IncludeAssets>
		</Reference>

		<PackageReference Include="FontAwesome6.Pro.Fonts" Version="*" />
		<PackageReference Include="Westwind.Utilities" Version="*" />

		<!-- Other packages you might want to use directly - if creating forms UI -->
		<!-- <PackageReference Include="MahApps.Metro" Version="*" />-->
		<!-- <PackageReference Include="Westwind.WebView" Version="*" /> -->		
	</ItemGroup>

	<ItemGroup>
		<Resource Include="icon.png" />
		<None Update="version.json">
			<CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
		</None>
	</ItemGroup>
</Project>
```

Additionally the addin creates an `Addin.cs`, `AddinConfiguration.cs` source files which hold the addin implementation and an optional configuration class. A `build.ps1` file can be used to package up your Addin into a `Build` folder ready for use in the Markdown Monster Addin registry.

Here's what the project should look like in Visual Studio:

![](/images/AddinReferencesInProject.png)

### Working with your Addin Class
If you need to do this manually create a new C# class that inherits from the **MarkdownMonsterAddin** class. The template creates a `SampleAddin` class in `Addin.cs` and provides the base infrastructure to load the addin on MM startup. It also sets up a toolbar button and `OnExecute()` handler you can implement to quickly add behavior to your addinand or you can choose to hook up and respond to additional events that are fired throughout the application lifetime.

This is a link [](https://west-wind.com)

The basic process is:

* Override the `OnApplicationInitialized()` method
* In that method hook up the Menu handler to invoke your add-in
* Override `OnExecute()` to handle the toolbar click

For reference, here is the default add-in implementation that gets generated,  with the `SampleAddin` as the new project name:

```csharp
using System;
using System.Windows;
using FontAwesome6;
using MarkdownMonster;
using MarkdownMonster.AddIns;
using System.Threading.Tasks;

namespace SampleAddin
{
    public class SampleAddin : MarkdownMonster.AddIns.MarkdownMonsterAddin
    {
       public override Task OnApplicationInitialized(AppModel model)
        {
            
            // Id - should match output folder name. REMOVE 'Addin' from the Id
            Id = "SampleAddin";

            // a descriptive name - shows up on labels and tooltips for components
            // REMOVE 'Addin' from the Name
            Name = "A sample addin that demonstrates how addins work in MM";


            // by passing in the add in you automatically
            // hook up OnExecute/OnExecuteConfiguration/OnCanExecute
            var menuItem = new AddInMenuItem(this)
            {
                Caption = Name,

                // if an icon is specified it shows on the toolbar
                // if not the add-in only shows in the add-ins menu
                FontawesomeIcon = EFontAwesomeIcon.Solid_Bullhorn
            };

            // if you don't want to display config or main menu item clear handler
            //menuItem.ExecuteConfiguration = null;

            // Must add the menu to the collection to display menu and toolbar items            
            MenuItems.Add(menuItem);

            return Task.CompletedTask;
        }

        public override Task OnWindowLoaded()
        {
            return Task.CompletedTask;
        }


        public override Task OnExecute(object sender)
        {
            MessageBox.Show("Hello from your SampleAddin Addin", "SampleAddin Addin",
                MessageBoxButton.OK, MessageBoxImage.Information);

            return Task.CompletedTask;
        }


        /// <summary>
        /// Fired when you click on the configuration button in the addin
        /// </summary>
        /// <param name="sender">The Execute toolbar button for this addin</param>
        public override Task OnExecuteConfiguration(object sender)
        {
            MessageBox.Show("Configuration for our sample Addin",
                            "Markdown Addin Sample",
                            MessageBoxButton.OK, MessageBoxImage.Information);

            return Task.CompletedTask;
        }


        /// <summary>
        /// Determines on whether the addin can be executed
        /// </summary>
        /// <param name="sender">The Execute toolbar button for this addin</param>
        /// <returns></returns>
        public override bool OnCanExecute(object sender)
        {
            return true;
        }
    }
}
```

This add-in simply displays a `MessageBox()` when you click the Toolbar button, which is a placeholder for any other type of operation you'd like to perform. More on that in a minute.

> #### @icon-info-circle Handlers are Async
> Please note that most of the handlers you can implement are **async methods** that return `Task`. This is because many operations in Markdown Monster require async access and this ensures you have access to the MM async context easily. Most examples don't implement `async` methods, but return `Task.CompletedTask` because the methods don't require any `await` calls and you'd get compilation errors. If you need to access `async` methods in your code using `await`, change the method headers to use `async Task` or `async Task<T>` to gain access to `await` functionality - it works either way. 

### Build the Project
With the Project Template and assuming standard install folders, the project should be ready to build and run. You can also start debugging by running the application in Debug mode, which should launch Markdown Monster as the startup executable.

> #### @icon-warning Build and Debug Failures
> If the project does not build or run, **make sure your paths are correct**. The new Add-in assumes you installed Markdown Monster in the default `%localappdata%\Markdown Monster` location and build your addin to the common folder location at `%appdata%\Markdown Monster\Addins` - if you used a different install folder or the portable installer, you'll have to adjust the project paths in the `.csproj` file by replacing all references to `$(localappdata)` and `$(appdata)` folders with your actual MM install and common folder paths.

When the project builds the the output is generated into the Markdown Monster Shared Settings folder and the `Addins` folder below that. The default build location is: `%appdata%\Addins\SampleAddin`.

### Default Toolbar and Menu Items
The template generated code creates the default toolbar button and menu item in `OnApplicationInitialized(model)`. That code sets up the Toolbar menu items for the toolbar icon as well as a menu option on the **Tools -> Addins** menu popup. 

If you don't want to display the menu item or configuration option - because your add-in maybe doesn't need any UI - simply disable the event handlers on the menu item explicitly:

```csharp
// don't show Configuration drop down button
menuItem.ExecuteConfiguration = null;
```

When you do this the toolbar button and menu item dropdowns are not displayed.

By default the toolbar button handler is routed to the  `OnExecute()` handler, which is a good starting point for most addins to test and interactively launch behavior.

#### What can you do with your Addin?
Add-ins can be as simple or as complex as you want to make them. The template only sets up the `OnExecute()` click handler routing, but there are many other things you can do in an Addin.

Addins may intercept document update operations and insert or modify content of the document. Others yet may pop up their own Forms and perform many user interface or conversion operations. Yet other ones like the KavaDocs add-in hook up entire documentation management system hooked in as an add-in.

To give you some ideas, here are a few things you can do from within an Add-in:

* Manipulate the active document or editor
* Insert or update text in a document
* Activate an open editor
* Load and save a document from disk
* Select a folder or file in the Folder Browser
* Monitor document updates and manipulate the text before saving/updating

#### The Addin Model
An top level addin instance, exposes a `Model` property that gives access to a host of powerful, top level properties that allow you to perform the above tasks and more. Here's what the live Model object looks like in the debugger:

![](/images/AppModelInVsDebuger.png)

Here are what some of the more common properties you might use:

* **ActiveDocument** 
The document holds the active document's content, as well as information about the file, document format and statistics and so on. It's also used to load and save a document.

* **ActiveEditor**   
Using the editor instance you can manipulate the editor's operation by selecting, inserting and removing text, searching etc. A huge number of editor commands are accessible both for the editor wrapper as well as the core editor surfaces (JavaScript). The most common editor operations revolve around selecting and updating or inserting text into the document.

* **OpenEditors/OpenDocuments**  
You can also access all the Open editors or Documents as a collection to find a specific open editor or document to work with rather than the active one.

* **Window (Main MM Window)**  
This object gives access to all of Markdown Monster's UI. You can gain access to the menu to add items for example, as well as gain access to the open editor tabs, the file and folder browser, the bookmarks window and so on. This is the entry point to the entire MM UI.

* **Configuration**   
This object holds all of Markdown Monster's many configuration settings. There are a number of nested objects that separate out the configuration functionality into things like Editor, Markdown, System etc. 

There are a lot more Model properties available and you can find out more about these objects and their sub-objects in the [Class Reference](VFPS://Topic/_55O1DXZIA) or by browsing the configuration file as JSON (go to Settings, then click on Edit JSON).

#### Implementing generic Addin Configuration
By default the Addin also creates a [configuration class](VFPS://Topic/_5520TLAV7) that you can use to hold configuration data specific to your addin. The configuration class can be easily persisted and is configured to handle loading and saving autmatically. You can add any properties to the configuration class and those properties are then accessible via `SampleAddinConfiguration.Current.Property`.

The `.Write()` method can then persist the configuration data to a JSON config file, or you can use `.Read()` to re-load configuration data from disk. The latter is useful if you edit the configuration setting as a JSON file, you can then update the current settings by reloading the settings from disk. The configuration data is stored in a JSON file in the common settings folder (ie. `%appdata%\Markdown Monster` by default) and is not deleted when the add-in is removed.

##### Simple Configuration Management via JSON File Editing
Most add-ins require some sort of configuration. For example, the [Azure Blob Storage add-in](https://github.com/RickStrahl/SaveToAzureBlob-MarkdownMonster-Addin) needs to store account information for any remembered blob stores and you'll need a place to hold this configuration.

Your addin project automatically generated a `Configuration.cs` class that you can use to add custom properties that can be persisted to disk. A very common way to handle add-in configuration is to write configuration settings to file when the add-in is shut down (`OnApplicationShutdown()`). To modify settings you can then simply open and edit the JSON configuration file in an MM tab and save it when you're done - intercepting the save operation to re-read the updated changes.

To put this all together in the Add-in looks like this:

```cs
// Opens configuration editing
public override Task OnExecuteConfiguration(object sender)
{
    // save current settings to file before editing
    SampleAddinConfiguration.Current.Write();

    // open the add-in config file in the editor
    var path = Path.Combine(Model.Configuration.CommonFolder,@"SampleAddin.json");
    Model.Window.OpenFile(path);  // opens file in a tab for editing
    
    return Task.CompletedTask;
}

// detect when we made a change to the configuration file in the editor
public override Task OnAfterSaveDocument(MarkdownDocument doc)
{
    await base.OnAfterSaveDocument(doc);

    // when saving check for our config file
    if (doc.Filename.Contains("SampleAddin.json"))
    {
        // re-read the configuration to update with changes
        SampleAddinConfiguration.Current.Read();
    }
    
    return Task.CompletedTask;
}
```        

If your add-in makes interactive changes to the configuration (like in a custom window) you should also write it out when the addin shuts down or when you exit your UI or other change operation.

```cs
public override Task OnApplicationShutdown()
{
    base.OnApplicationShutdown();
    SampleAddinConfiguration.Current.Write();
    
    return Task.CompletedTask;
}
```
### Addin Binaries Location
Addins run out of the `%appdata%\Markdown Monster\Addins` folder by default. Each addin gets its own folder which contains the binaries to load the add-in.

The project template automatically points the build output to this folder in the project settings:

```xml
<OutDir>$(appdata)\Markdown Monster\Addins\SampleAddin</OutDir>    
```

#### Addin Dependencies
If you are explicitly using any dependencies in your code - including depedencies that Markdown Monster explicitly loads - make sure to add the appropriate NuGet packages or references. 

If you're explicitly using features in packages that Markdown Monster already uses add the packages like this:

```xml
<ItemGroup>
    <PackageReference Include="MahApps.Metro" Version="*" />
</ItemGroup>
```

This will provide a compile time reference but it won't output the package content into the Addin output folder.

If you explicitly need to deploy extra assemblies that MM doesn't already use, you need to explicitly force the dependencies to published into the addin output folder:

For example, in the Weblog Addin I'm explicit referencing an XmlRpc library like this:

```xml
<PackageReference Include="Kveer.XmlRPC" Version="1.2.2">
  <IncludeAssets>all</IncludeAssets>
</PackageReference>
```

The `<IncludeAssets>all</IncludeAssets>` element ensures that the library and its depedencies are output into the addin output folder.

#### Unloading Markdown Monster to see Addin
If MM is running and the addin is loaded you will have to stop all instances of Markdown Monster before you can recompile the files. Addins load when Markdown Monster starts, so you have to restart to see your newly built addin.

### Test your Add in
At this point you should also be able to run your add-in. When you do, you should now see something like this:

![](/images/AddInRunning.png)

Note the bullhorn icon in the toolbar on the right which is the default icon for this add-in as specified in the initialization code but you can change that easily to another FontAwesome or a real image icon.  If you click the Toolbar button, you should see the dialog box as shown which verifies the add-in works.

The dropdown to the right provides for executing the addin, executing the configuration handler or uninstalling the add-in.

### Debug your Add in
The project is set up with a custom `Properties\Launchsettings.json` file that allows you to run or debug the application from Visual Studio or any other development tool that uses this file to determine which application to run. 

> The project runs `MarkdownMonster.exe` from the default install location in `%localappdata%\Markdown Monster` - if you installed in a different location you'll need to change `Launchsettings.json'` to reflect the alternate install path.

In Visual Studio you can simple run your project in debug mode and set breakpoints as needed and the debugger stops at the appropriate place in the code:

![](/images/AddinDebugging.png)

### Package your Addin
If you're building your addin only for your personal use, there's nothing else you need to do. You can simply build into the `Addins` folder and you're done.

#### Updating version.json
Make sure that you update `version.json` in your project to:

* Provide a new `version` number for your build
* Specify a `minVersion` to require a minimum Markdown Monster version
* Set the `updated` publish date of your addin

#### Publishing to the Addin Registry
Once you have debugged your addin locally you can optionally share it in a GitHub repository and submit it to the [Markdown Monster Addin Registry](https://github.com/RickStrahl/MarkdownMonsterAddinsRegistry).

An addin project that is published to the Registry needs to be in a specific format and you can use `build.ps1` to create a `Build` folder in the root of the project. The folder contains the binaries of the addin in zipped up format as well as a `version.json` and `icon.png` file that identify the addin for the Addin Manager.

There's more information on how to publish your Addin to the Addin Registry on the GitHub site that hosts the addins.

[Markdown Monster Addin Registry](https://github.com/RickStrahl/MarkdownMonsterAddinsRegistry)

### And you're off to the Races!
And voila with that you've hooked up your Add-in. You can now run any .NET code necessary to manipulate the markdown content, bring up your own UI and or transfer rendered output to a server for example.

We'll look at some of the things you can do in the next topics.

* [Accessing and manipulating the Active Editor Document](VFPS://Topic/_4NF02Q0SZ)
* [Bringing up UI from your Markdown Monster Addin](VFPS://Topic/_4NE1CH7WA)