If you are creating an addin that performs some non-visual operation it's often necessary to provide some feedback to the user. You can do this in two ways:

* Display a message in the Main Window's Status Bar
* Use the Main Windows Console Output Panel


## The Status Bar
The status bar provides a simple single message display mechanism as part of the main application. It's displayed at the bottom of the window and typically displays a **Ready** message and icon:

![](/images/StatusBarReady.png)

The status bar is accessible with a number of methods on the `Model.Window` class:

* **ShowStatus()**  
The low level method that has a number of parameters for many options. We recommend you don't call this unless you have specific needs and instead use one of the other status methods.

* **ShowStatusError()**  
Displays a red warning icon and the status message in red.

* **ShowStatusSuccess()**  
Displays a green checkmark icon and regular status message.

* **ShowStatusProgress()**   
Displays an orange spinning progress icon and regular status text.

All methods have default timeouts (6000ms by default) that keep the message displayed active for the timeout period, before reverting back to the **Ready** status message shown above. Parameter control the icon, the color and timeout. The `ShowStatus()` method has additional overloads, but all methods eventually call `ShowStatus()` to actually update the status bar text, icon and duration.

```cs
// Green icon
Model.Window.ShowStatusSuccess("Hello World",3000);

// Red Icon
Model.Window.ShowStatusSuccess("Danger Will Robinson",5000);

// Orange Spinning Icon
Model.Window.ShowStatusProgress("Updating document...");
```

> #### @icon-warning Status Bar Methods are Asynchronous
> Commands are asynchronous, so if you run multiple commands one after the other, only the last one is likely to display. For timeouts the last one assigned is the one that runs - other already active timeouts are cleared.

## The Console Output Window
The Console Output Window by default is hidden, until it is written to by the application or an addin. The Console Output window can be used to show many messages for an addin that performs a number of actions and needs to display progress or other status information.

The following demonstrates how the Console can be accessed from an Addin (The Snippets Addin in this case):

![](/images/ConsoleOutputPanel.png)


To create Console Output, an addin can use the `Model.Console` property to write output:

```cs
Model.Console.WriteLine("Hello World " + DateTime.Now.ToString("HH:mm:ss"));
Model.Console.WriteLine("Hello Red World", System.ConsoleColor.Red);
```

If the Console is not visible it's made visible and the output is - line by line - written to the console. The Console has buttons to clear the content and close the panel.

Note that you can write output using colors, using either `System.ConsoleColor` or `System.Windows.Media.Brushes` for color.

> The `Console` object is not a standard `System.Console` object, but rather a simplified output mechanism as output is sent into the custom textbox based output window.