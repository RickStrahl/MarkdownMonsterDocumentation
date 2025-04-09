When working with wide monitors it's quite common to get a feeling of **too wide** of a wall of text when editing. Maxing the editor on a 4k screen can really overwhelm the user with too much text. Studies show that there's an optimal width for reading text which is generally somewhere around 120 characters per line max.

Markdown Monster lets you configure how wide is too wide, or lets you go full bore if want to take in all the text you can get at once.

### Layout Modes
To make this easier to manage Markdown Monster has two editor layout modes:

* Full Width Layout
* Centered Layout

You can toggle between Full Width Layout and Centered Layout Modes on an off using **View -> Toggle Centered Layout** from the menu.

Full Width Layout stretches the entire width of the editing surface, while Centered Layout uses a max width to limit the maximum width that the editor's content can expand to before wrapping. Any excess width is then evenly split with padding, so the actual content is in effect centered on the editor canvas.

You can configure the explicit settings using the explicit configuration properties in **Tools -> Settings**:

* Editor.Padding
* Editor.CenteredMode
* Editor.CenteredModeMaxWidth

### Padding
Determines the padding around text in Full Width Layout mode. This is the horizontal padding around the editor text when text fills the entire editing area. The value is a fixed pixel width and defaults to 15 pixels.

Padding is ignored when using `CenteredMode` and the width of the edit panel is larger than the `CenteredModeMaxWidth`.

Set with the `"Padding": 15` configuration setting.

### CenteredMode and CenteredModeMaxWidth
You can enable Centered Mode by setting the `"CenteredMode": true` in the Settings. To go along with that setting you can then specify the width of the centered content using the `"CenteredModeMaxWidth": 1080` property which is given in pixels. The default width is 970 pixels.

The `CenteredModeMaxWidth` is used to dynamically calculate any padding that is applied to the editor surface when the width of the edit pane is larger than the max width specified. Any size that is larger is padded, effectively providing some 'white space' around the content in the editor.

Here's what the Centered Mode looks like when set to 970 pixels on an approx 2k total window size (including preview/folder browser):

![](/images/MaxWidthPadding.png)

Notice the padding around the text in the center which increases as you widen the window, and shrinks down to the max width. If the max width is not exceeded the editor falls back to the fixed side margins at which point the `Editor.Padding` is applied.