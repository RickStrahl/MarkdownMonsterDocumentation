Markdown Monster supports capturing Screen Captures of Windows and Screens via both a built-in capture utility and the popular [SnagIt Screen Capture Utility from Techsmith](http://techsmith.com/snagit). Both provide integrated support for snapping a screen shot of a window, control or screen, save the file to disk and then reference the saved as a Markdown image link.

* [Alt-PrtScn and Paste Image](#PrtScn)
* [Built-in Screen Capture](#Built-in)
* [SnagIt Screen Capture](#SnagIt)

<a name="PrtScn"></a>
### Alt-PrtScn and Paste Image
One of the easiest ways to capture screen shots on the desktop is to use Windows' built-in screen capture tooling by using `Alt-PrtScn`:

* Select a window on the desktop
* Press `alt-PrtScn` 
* Goto the Markdown Monster Editor
* Press `ctrl-v` to paste the image into the editor
* Select a file name to save to

This is a quick and easy way to embed a screen capture into your document and it works well if all you need is to display Window content.

If you need to display a mouse cursor or active UI like drop downs or selections, you can use one of the other two capture options.

<a name="Built-in"></a>
### The Built-in Screen Capture
The native screen capture form is a simple utility that lets you capture desktop windows into screen shot images:

![](/images/screencaptureform.png)


There are two configuration options for the capture:

* **Capture Delay**  
You can specify a delay before the capture starts to allow you to manipulate the UI before capture. Capture delays are great if you need to highlight a control or show dropdown list etc. When a capture timeout is set the capture is delayed, showing a count down timer in the lower right corner of your main screen.

* **Capture Mouse Cursor**  
You can optionally capture the mouse cursor with your capture.

Both of these options are a good reason to use a dedicated capture over using `Alt-PrtScn` window captures.

### Doing a Screen Capture
To start a screen capture click on the **Click to Start** button.   The capture highlights whatever window the mouse cursor is over and you can click to select the window to capture.

![](/images/ClassicScreenCapture.gif)

Once selected the capture content is displayed in the capture form. From there you can save it and/or open it in your configured editor.

To save the image click on the **Save** toolbar button, to write out the image to disk and embed it into your Markdown text as you exit the capture form.

You can also click on **Save and Edit** which performs the same teps of saving and embedding, but also opens the saved image file in the configured **ImageEditor**.

The screen capture form also includes a few additional features, like the ability to paste an image from the clipboard, copy a captured image to the clipboard, and opening the saved image in the configured **ImageEditor**.

<a name="SnagIt"></a>
### SnagIt Screen Cature
In order to use the SnagIt screen capture features, make sure you enable it first:

* Click on the Down Arrow next to the Screen Capture Icon 
* Select Screen Capture Configuration
* Check **Use SnagIt when available**

![](/images/snagitcaptureaddin.png)


To start a screen capture click on the Capture icon (the monitor icon in the toolbar) to bring up SnagIts capture UI:

![](/images/SnagItScreenCapture.gif)


SnagIt offers a number of different capture options. The most useful is the **All in One** feature which lets you capture windows, objects or free form rectangular selections. Other options include windows, menus, scrolling windows, totally freeform shapes and even printer output.

The options are pretty self explanatory.

Click **Save** or **Capture** depending on whether you have the preview or configuration option and go.

### SnagIt Editor Preview
If you have the **Show Preview Window** option enabled the captured image is shown in the SnagIt Editor. In the editor you can crop and modify the image, add annotations, shadows, perspective and otherwise apply effects and features to the image.

Here is an example of an image that is marked up with annotations:

![](/images/SnagItEditor.png)

When done click the **Finish** or **Cancel** button to embed or abort the captured image.

### Image Embedding
Images for either capture type are embedded as standard Markdown images in the format of:

```Markdown
![](/images/screenshot.png)
```
using **relative paths to the image** if the path can be expressed as a right side relative path. Otherwise the full path is used. 

You can edit the embedded markdown as necessary to add a title or modify the path.