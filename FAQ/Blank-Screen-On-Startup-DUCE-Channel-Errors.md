We have found some instances where Markdown Monster will start with a blank main screen when first loaded:

![](/images/faq_blankscreen.png)

The application is running and responsive, but the screen does not render properly. Dragging the window to another screen often can bring back the properly rendered window.

The issue is caused by a combination of video drivers and certain monitor combinations. We've specifically isolated the following drivers:

* nVidia Quadro (most versions)

### Workaround: Turn off Hardware Assisted Rendering
The issue itself is caused by the DirectX rendering used by WPF and the workaround is to turn off hardware assisted video rendering.

In Markdown Monster you can disable hardware rendering as follows:

* Go to **Tools -> Settings**
* Set the `DisableHardwareAcceleration` to true
```json
"DisableHardwareAcceleration": true
```

This is a hack that disables offloading of video rendering to the GPU and doesn't rely on the specific video card hardware and driver. It'll also slow the UI Chrome rendering down, but for Markdown Monster there's very little of that that actually affects the application for it to matter.

This fixes the blank startup screen in most instances. It can also fix random hardware crashes.

For more info on this issue see the original bug report and resolution:

* [Github Issue: Blank Screen](https://github.com/RickStrahl/MarkdownMonster/issues/136)