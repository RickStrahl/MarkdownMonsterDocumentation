There are a number of different ways that you can export rendered your Markdown content as rendered HTML.

* Using the **File->Save To->Save To Html** Dialog
    * Export the **Raw Html Fragment**    
    * Export as **Packaged HTML file**
    * Export as **HTML File with loose Assets**
    * Export as **Packaged Zip File**
* Use **View In Browser** and **Save As Html** from Browser
* Use **Copy Selection as HTML** to copy selected Markdown text as HTML to the Clipboard

### Using Save As HTML
This option lives at **File->Save To->Save to HTML** and it allows you to save your Markdown content as a rendered HTML in a few different ways:

![](/images/saveashtml.png)


Here is what each of those options does:

#### Save Raw HTML Fragment
The most basic way to save is to save the raw HTML output from the rendered markdown **as is**. 

Choose `Raw HTML output only (Html Fragment)` if you want just the raw rendered HTML output from your markdown and save it to file. The output contains only the output from the actual Markdown text, without the wrapping HTML document or preview formatting - it's an **HTML fragment only**. Images, related CSS or Javascript **are not embedded or copied** - this is literally just the raw HTML that was generated.

This is useful for copying the raw HTML to server applications that provide their own styling or hold all relative resources on the actual Web site in file accessible folders.

**Use Case**:  
*Raw export for use in applications that provide styling and related content - such as Weblogs, Documentation etc.*

#### Save as self contained HTML Page
Allows you to save the document and all of associated resources as a **single large HTML file** with all dependencies embedded into the HTML as inline resources. All images, scripts, CSS, fonts etc. are embedded into the document as embedded binary data. Because all resources are embedded this file can often **be very large** as all the support libraries like Bootstrap and FontAwesome are embedded. The output is based on the current preview theme.

The packager imports local dependencies, as well as web based resources and embeds them into the document. Because the file is completely self contained in a single `.html` file you can move the file to a new location and it should still render correctly.

**Use Case**:  
*Fully self contained file that you can email and share, or publish as a static file on a Web site. File tends to be very large as all resources are embedded.*

#### Save as HTML Page in Folder with Loose Assets
Allows you to save the HTML document to file, with all related dependencies copied to disk in the same folder. All images, CSS, Scripts and fonts are also created in the same folder.

> It's recommended that you create the generated HTML in a new empty folder so the HTML and its dependencies are easily isolated and can be zipped or moved as a group. The **target folder is not cleared first** if it exists.

**Use Case**  
*Useful for hosting on a static Web site or simply for archival purposes of the full content.*

#### Save Zip Package
This performs basically the same operation as the Folder with Loose Assets output, but it packages the resulting files into a packed Zip file that you can copy around more easily. To use the output, simply unpack the Zip file into a folder and the rendered HTML should find all of its dependencies to render self contained.

**Use Case**  
*Same scenario as loose files but for emailing, or moving between machines and for archival purposes.*

### Copy As HTML
You can use the editor's Context Menu **Copy As Html** or **ctrl-shift-c** to copy the current Markdown selection as an HTML fragment to the clipboard. To select the entire document use **ctrl-a** then **ctrl-shift-a** to copy the generated HTML to the clipboard.

This can be quite useful if you want to use MM as your Markdown editor for pushing content into HTML based input controls.

### Exporting HTML using Browser Save As
The above options are native to Markdown Monster itself. The following is a technique you can use with your preferred browser, which may render the HTML differently and under some circumstances may do a better job with very complex HTML output.

To do this:

* Open your Markdown Document
* Make sure the Preview browser
* Use the Preview Browser's Context Menu:  
  **Show In external Web Browser** or  
  **View->View in Web Browser**
* HTML opens in Web Browser
* In the external browser choose Save As...
* Pick a file location and save
* Open the `.html` file from the local folder

Depending on the browser you get options to save a single document of just the HTML, or HTML plus all dependencies in a folder, similar to the behavior described for MM above.