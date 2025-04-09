﻿When editing very large documents - especially those that include a large number of code snippets - you may find that the Markdown editor starts to have issues with the preview refresh and potentially also some editor hesitation while the preview is being refreshed.

The performance slowdown is due to the time it takes to render the large HTML document in the preview browser - it's the time the HTML DOM takes to refresh the display. Due to architectural limitations of the Web Browser Control used by this application the preview ties up processing while the preview is being rendered. For normal sized documents up to a megabyte or so, this process is pretty fast and practically unnoticed, but once documents reach a certain size, the preview loading takes so much time that it effects the rest of the editor.

There are a few workarounds that allow you turn off automatic preview refreshing:

* Less frequent Preview Refresh Intervals
* Turn off Preview Refresh
* Turn on Navigation Only Preview Refresh


### Less Frequent Preview Refreshes
The preview timeout is fired when you pause typing for a specified amount of time. By default this timeout is ~200 milliseconds, which is only a brief break in typing and that works well for most documents.

To mitigate huge document rendering mentioned above MM slows preview updates considerably when documents reach 2000 lines in the editor. This means you have to pause typing for 2 full seconds before the preview will refresh. This is meant as a very deliberate action.

Note that the preview will likely still render slowly for the large document and may still affect typing if you start typing again while the preview is still updating. But since the updates happen much less frequently you can continue to type text at normal input speeds in most situations without getting interrupted by the normal refresh that fires every 120ms or so.

### Workaround - Use Preview Refresh `None` or `Navigation Only`
Another option is to use Preview Refresh `None` or `Navigation Only` neither of which will automatically update the document as you type. Instead you can use the **Edit -> Refresh Preview (Alt-E-R)** to explicitly refresh the preview.

This allows you to type your text without interruptions and whenever you're ready to see the updated preview you can use the menu or hotkey to see the changes at the cursor.

You can set the Preview Mode using the icon on the very right of the Status Bar next to the size corner to select the Preview Sync Mode or the `PreviewSyncMode` property in the Markdown Monster Settings:

```json
{
    "PreviewSyncMode": "NavigationOnly"  // or "None"
}
```

Note that `Navigation Only` will show you document navigation changes so you can still scroll through the document and have the preview pane update. However, if you've typed new text it's possible that the preview might be out of sync, so if you type it's recommended to use the explicit **Preview Refresh** menu option to force a refresh to ensure the document is up to date when navigating.

> @icon-info-circle We recommend using **Navigation Only** as the mode for huge documents.

### Workaround - Turn off the Preview
If this problem affects your regular typing input, you can optionally **turn off the Preview Pane (F12)**. Turning off the previewer while you're typing lets you edit your document at full speed without any slow downs whatsoever, and you can press F12 to preview the document when you're ready to see the current changes. Press F12 again to hide the preview.


### Workaround - Break up your Documents
This may be obvious, but we don't recommend creating massively large single Markdown documents, but rather to break up your content into logically related documents along with a Table of Contents to consolidate multiple documents into a more manageable documentation solution and structure.

Not only is it easier to edit and find content in smaller documents, but it also makes it much easier to collaborate for multiple people as document changes can be much more focused.

### We're looking into it
We realize this isn't ideal and we're looking into alternatives for the future. Unfortunately other alternatives like DOM diffing have other problems (slow and buggy), but we're still reviewing options.

Then again, documents so large that they actually cause this problem tend to be very rare and it's unlikely you're going to hit this particular problem with typical content.

> #### @icon-info-circle Break up your Content
> Note: When talking about huge documents we're talking of documents that are larger than 500k or include lots of code snippets or other script expanded elements.
>