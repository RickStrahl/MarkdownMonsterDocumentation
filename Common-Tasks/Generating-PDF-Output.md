Markdown Monster renders Markdown text into HTML output when it transforms your Markdown document, and you can print the rendered HTML to a printer or a PDF document using several different mechanisms.

The following uses the preferred  **Save As Pdf Dialog** to render to Pdf output:

![Pdf Output Generation](/images/PdfOutputGeneration.png)

There are a number of ways to produce Pdf output in Markdown Monster:

1. **File -> Save to - > Save to Pdf** menu option  
 or the **Pdf Output button in the Toolbar**
2. **File -> Print Output -> Save As Pdf** Browser Print Dialog  
or **Print from the Previewer Context Menu**
3. **View in external Browser and Print As Pdf** from there

## Generate a PDF using the Save As Pdf Dialog
This is the **preferred mechanism for printing PDF output** as it's optimized for Pdf generation and has more options than using the built-in Web Browser print tools.

The easiest way to create a PDF document is to use this dialog to generate a PDF document:

![Save as Pdf](/images/saveaspdf.png)

> Save As Pdf uses the *Chromium WebView Engine* to print the rendered HTML document to Pdf, which uses the same engine used by any Chromium browser like Chrome, Edge, Brave, Vivaldi etc.

#### Using Print Themes
It's now possible to select  **any Preview Theme** available for previewing Markdown content. 

The default theme that is selected is **Pdf Output** which is a very basic theme geared towards plain print output that is universally compatible across platforms. You can however choose to use any of the available preview themes most of which work fine for print output as well.

> **Note:** Dark background themes require custom margin background color selection, and custom Html Header and Footer Templates to customize margin foreground color. *(see [Html Templates](#htmltemplates) below)*

#### Margins
Margins are not part of the generated Markdown Html output, rather the Html content is printed inside of the margins with the margins wrapping around the content. 

There are several important things about Margins to understand:

* Margin Color is set by the **Margin Background Html Color**
* Headers and Footers print in the Margin area
* Non-white margins require custom Html Header Templates    
  <small>*(at minimum to customize the text color - more below)*</small>

#### Margin Background Color
Print margins are separate from the Html output and styled individually and so the background color for margins has to be explicitly set in the **Margin Background Html Color**. The default is **white** or **#FFFFFF** - you can use any Html color name or hex color expression.

If you choose to use a dark background for your margins, you have to use a custom Html Header with an Html template that explicitly sets the foreground color.

The following figure demonstrates generating a PDF using the *GitHub Dark* theme.

![Margins And Background Color](/images/MarginsAndBackgroundColor.png)

You have to set:

* The Margin Background Color to match the document background (#0d1017)
* Custom Html Header Template that includes the foreground color

#### Headers and Footers
The print engine outputs headers and footers in the margin area of the output. You can specify headers and footers in two ways:

* **Plain Text**  
This generates headers and footers in fixed locations, specifically centered at the top for headers and in the bottom right corner for footers.  Text can contain variables using `[variableName]`.

* **Html Templates**  
Html Templates give more control and allow you to fully customize headers and footers by rendering them as an Html fragment - a `<div>` tag. You also need to use a template if you need to change the default color of header and footer text to something other than the default black. You can embed variables using `<span class='variableName'></span>`

#### Embeddable Variables
You can embed variables into headers and footers using different mechanisms depending on whether you provide plain text or an Html template:

* Plain Text: `[variableName]`
* Html Template: `<span class='variableName'></span>`

Available embeddable variables are:

* title
* date
* pageNumber, totalpages
* page, topage *(same as above)*

#### Html Templates
If you want full control over your headers and footers, or you need to print dark colored headers and footers, you can use Html Templates to render the header and footer.

> You can click the blue pen icons to embed default Html templates that you can modify.

Some template suggestions:

**Basic** 

```html
<!-- header -->
<div style='font-size: 11.5px; width: 100%; text-align: center; color: black'>
    <span class='title'></span>
</div>

<!-- footer -->
<div style='font-size: 10px; clear: all; width: 100%; margin-right: 3em; text-align: right; color: black'>
   Page <span class='pageNumber'></span> of <span class='totalPages'></span>
</div>
```

**Github (background: `#0d1017` )**

```html
<!-- header -->
<div style='font-size: 11.5px; width: 100%; text-align: center; color: white'>
    <span class='title'></span>
</div>

<!-- footer -->
<div style='font-size: 10px; clear: all; width: 100%; margin-right: 3em; text-align: right; color: white'>
   Page <span class='pageNumber'></span> of <span class='totalPages'></span>
</div>
```

**Custom Layout with top left and right panels**

```html
<!-- header -->
<div style='font-size: 11.5px; width: 100%; text-align: left; color: white; display: flex; padding: 0 1em '>
    <div style='width: 50%'>
        <span class='date'></span>
    </div>
    <div style='width:50%; text-align: right'>
        <span class='title'></span>
    </div>
</div>

<!-- footer -->
<div style='font-size: 10px; clear: all; width: 100%; margin-right: 3em; text-align: right; color: black'>
   Page <span class='pageNumber'></span> of <span class='totalPages'></span>
</div>
```


## Built in Printing
Alternately you can use the built-in Browser PDF printing facility either in the Preview browser in Markdown Monster or in your system Web Browser.

To do this:

* Open your document
* Make sure the Preview is open
* Press `ctrl-P` or **File->Print Output->Save to Pdf**
* Pops up browser's Print Dialog
* Select **Save as PDF**

This brings up the browser's print dialog that lets you print to PDF output:

![](/images/PrintDialog.png)

You can also use this mechanism to print output to a printer.

> Note that in-browser printing uses the same print engine as Save As Pdf, but it lacks some customization features, like creating custom headers and footers, and there's no explicit support for auto-page break management. It's recommended you use the Save As Pdf Dialog instead.

### Using an External Web Browser Instance
If you don't want to use the built-in printing based on Microsoft Edge Chromium's WebView, you can also use an external browser, by choosing **File -> View in Web Browser** or **Alt-v-b** which opens your Windows configured Web browser.

You can then use that browser's print facility to print the document to a printer or PDF document and use your favorite browser's facility to perform print tasks.

### PDF Output Generation is not Perfect
Please keep in mind that **PDF output generation is not pixel perfect** compared to your HTML output. It works well for most use cases, but the output generation for each mechanism has some limitations.


### Also Consider Packaged HTML Output
If you want true HTML representation of your Markdown Content you can also use the **Save to -> Save To Html** option and [Save Markdown Output as HTML](VFPS://Topic/_57W02I1F6).

There are options to create packaged HTML that is self contained in a single file, that makes it easy to create local content that can be viewed as HTML in any browser getting the same exact output that you are seeing in the preview without having to deal with Pdf page-break semantics. 

> One downside of this approach is that self-contained Html files tend to be very large in size.