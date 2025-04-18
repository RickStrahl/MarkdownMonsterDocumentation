Preview Themes control how the Preview Window renders your Markdown text into HTML. Because Markdown is a text representation of an HTML document, some sort of engine has to render the Markdown into HTML and then apply HTML and CSS styling to render that HTML into what you see in the browser.

This process **may vary significantly** depending on where you display your Markdown. For example, GitHub renders Markdown very differently than BitBucket. If you're using Markdown on your blog, you probably also have some very custom styling and potentially use a completely different Markdown parser to parse Markdown into HTML.

While there will always be some differences between Markdown implementations on different platforms, Preview Themes can help you create or use themes that more closely match your target Markdown platform's layout and styling.

## Changing Preview Themes
In Markdown Monster you can easily change themes in the editor's UI by using the status bar theme selector on the lower right:

![](https://github.com/RickStrahl/ImageDrop/raw/master/MarkdownMonster/PreviewThemes.gif)

Theme settings are stored in the configuration under:

```json
{
    "Preview": {
        "PreviewTheme": "GitHub"
    }
}
```

You can easily flip between the provided themes which include `Github`, `Github Dark`, `Dharkan`, `Blackout`, `Medium`, `Westwind` and `Hipster`. It's also quite easy to create **custom themes** by copying and modifying existing Preview Themes.

> ##### @icon-info-circle If you Customize create a new Theme!
> Default themes are installed and updated with Markdown Monster releases, so if you make changes in any of the default themes, any changes can and will be overwritten by updates. 
>
> To avoid this issue, **always** create a new theme from an existing one by copying the theme to a new folder. Give it a descriptive name and it will show up in the drop down list next time you restart. 
>
> Any custom themes should be created in the `%appdata%\Markdown Monster\PreviewThemes` folder.  

## Theme Customization
A theme is nothing more than a sub-folder in the `PreviewThemes` folder of your **Markdown Monster installation path** which typically is `c:\Program Files\Markdown Monster\PreviewThemes\Theme-Name` (*the base folder may vary depending on where MM is installed*). 

> #### @icon-warning Customized Themes should go into your Settings Folder
> For your own custom themes you create or extend, there's a separate folder in the Markdown Monster configuration folder which typically lives in `%appdata%\Markdown Monster\PreviewThemes\Theme-Name`.

The easiest way to find files for the active Preview Theme is by using the Previewer's right click Context Menu and the Edit Preview Theme menu item:

![](/images/PreviewThemeFromContextMenu.png)

That folder contains a `Theme.html` and related `Theme.css` file which make up the theme. There's also a `../scripts` folder that contains a few dependencies like FontAwesome for icon support and HighlightJs for code sytnax highlighting.

Here's what the PreviewThemes folder looks like:

![](/images/PreviewThemeFolder.png)

You can easily create custom Preview Themes or change existing themes by simply changing the HTML and CSS files that are provided.

### How Themes work
Themes are found based on the folder name in the `PreviewThemes` folder. Any sub-folder in the `PreviewThemes` folder will be available in the Preview theme selector:

![](/images/PreviewThemeSelections.png)

Any folder you add to `PreviewThemes` automatically shows up in this dropdown list. A theme folder is expected to hold `Theme.html` file which is used as a template to render the markdown by essentially embedding the rendered Markdown into the base page HTML layout. You can think of `Theme.html` as the site chrome or master layout. This page is mostly boiler plate, but you can customize it to add custom CSS or scripts etc. 

The HTML in this file is minimal as most of the HTML comes from the rendered Markdown, but the default template includes a link to `Theme.css` which provides the page styling, as well as links to the dependent scripts and FontAwesome icon CSS:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <base href="{$docPath}"/>
    <title>{$docTitle}</title>
    <meta http-equiv="content-type" content="text/html; charset=utf-8" />
    <meta charset="utf-8"/>

    <link href="{$themePath}..\scripts\fontawesome\css\font-awesome.min.css" rel="stylesheet"/>
    <link href="{$themePath}Theme.css" rel="stylesheet"/>

    <script src="{$themePath}..\scripts\jquery.min.js"></script>
    <link href="{$themePath}..\scripts\highlightjs\styles\vs2015.css" rel="stylesheet"/>
    <script src="{$themePath}..\scripts\highlightjs\highlight.pack.js"></script>
    <script src="{$themePath}..\scripts\highlightjs-badge.js"></script>
    <script src="{$themePath}..\scripts\preview.js" id="PreviewScript"></script>

    {$extraHeaders}

</head>
<body>
<div id="MainContent">
  <!-- Markdown Monster Content -->
  {$markdownHtml}
  <!-- End Markdown Monster Content -->
</div>

</body> 
</html>
```

If you want to add site branding or other items, in order to match an online site that will eventually host your Markdown you can add it around your Markdown content. **Just make sure to leave the `<div id="MainContent"></div>` in your document**, as that's where MM expects to Markdown content to go - some of the script code depends on the tag name and block tags to update content efficiently.

If you create a new theme, maintain the overall structure of this document. Typical customization just involves modifying the `Theme.css` styling, but some people like to add site branding into the preview and for that you can customize `Theme.html`.

There are a four template variables:

* **{$markdownHtml}**
This is where your rendered HTML is injected.

* **{$themePath}**  
This is the physical disk path to the preview folder (with a trailing slash). Markdown Monster renders HTML from this template into the folder where the Markdown file lives so that it can find any relative images and links properly. In order to find the related theme resources they have to be known and `{$themePath}` provides this known location.

* **{$docPath}**  
This is the HTML base path for the rendered HTML which by default is `./` (ie. the current path), but it can also be a custom value that is overridden. This value can be changed to allow referencing an external location like a Web site and can then render related resources like images or styling from those locations. `docPath` can be changed per document via [YAML properties and via Project settings](VFPS://Topic/_5FZ0OZKLN) - or if your template always relies on external resources you can just hard code the `basePath` directly in the HTML.

* **{$extraHeaders}**  
These are headers that can be set by `RenderExtension`s or addins that interact with the render process.

Make sure these values are provided in any template changes you make as these values are set during the render process and are also accessible to Addins and RenderExtensions that customize the render process.

### Custom Themes for Custom Preview Displays
Some of the things you can do is create custom templates that more closely match the display of your target platform. For example, you might want to match the styling of your Blog, or your documentation engine. 

Here's an example of a custom template that displays documentation content:

![A custom Theme for Documentation](/images/CustomThemeWebSurgeDocumentation.png)

### Creating a new Local Theme
Local themes simply use local resources for the CSS styling as shown in the last example. The CSS is linked directly from a local resource. This is the easiest way to deal with resources.

To create a new theme:

* Copy an existing folder from `<install folder>\PreviewThemes`
* Copy the folder to the Markdown Monster Common folder at:  
  `%appdata%\Markdown Monster\PreviewThemes` (or a custom location if you chose one)
* Rename the folder to a new name - that name is displayed in the themes dropdown
* Modify the `theme.html` or `theme.css` files to customize

### Web Themes
You can also reference Web resources directly from your `Theme.html` page. For example, you might want to use the theme from your Weblog so your preview looks exactly like the blog you're going to post from your markdown so you can link in the CSS stylesheet from your site. Note that you probably still want to use the default CSS style sheet to handle some formatting that is not covered by your online style sheet, but if it is to display your markdown the CSS should have most of the same functionality.

You can simply link an external stylesheet to make that work. However, you probably will still need a little bit of extra CSS to format the base document.

For example, I have a custom West Wind theme that has the following `Theme.html` page:

```html
<!DOCTYPE html>
<!-- saved from url=(0016)http://localhost -->
<html lang="en" xmlns="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="utf-8" />    
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <link href="{$themePath}..\scripts\fontawesome\css\font-awesome.min.css" rel="stylesheet"/>

    <!-- link style sheet from the Web site -->
    <link href="https://weblog.west-wind.com/App_Themes/Standard/Standard.css" type="text/css" rel="stylesheet"/>
    
    <!-- small amount of fixups -->
    <link href="{$themePath}Theme.css" style="text/css" rel="stylesheet" />
</head>
<body>
    <div id="MainContent" >
        {$markdownHtml}
    </div>
    <script src="{$themePath}..\scripts\jquery.min.js"></script>
    <link href="{$themePath}..\scripts\highlightjs\styles\twilight.css" rel="stylesheet" />
    <script src="{$themePath}..\scripts\highlightjs\highlight.pack.js"></script>
    <script src="{$themePath}..\scripts\preview.js"></script>
</body>
</html>
```
Notice the link to the external style sheet on [weblog.west-wind.com](http://weblog.west-wind.com). I still use a local theme.css to style the toolbar and the main HTML page padding:

```css
html, body {
    padding: 5px 20px 5px 10px !important;
    margin: 0;
} 
body::-webkit-scrollbar {
  width: 0.7em;    
}
body::-webkit-scrollbar-thumb {
  background: #999;
  border-radius: 0.2em;
}

@media(min-width: 970px){
    html,body{
        font-size: 1.05em;
    }
}
```

Very minor obviously but this ensures I get the right document margins and the nicer looking scrollbars in the preview.

Another option is to simply download the remote CSS and use it locally rather than load it from the Web site and then reference the local copy:

```html
<link href="{$themePath)Standard.css" type="text/css" rel="stylesheet"/>
<link href="{$themePath}Theme.css" style="text/css" rel="stylesheet" />
```

### Change the Code Snippet Theme in your Preview Theme
The previewer supports code snippets using the popular <a href="https://highlightjs.org/" target="top">highlight.js</a> and the corresponding syntax language formats. This is compatible with GitHub for common languages.

If you want to alter the code theme you can change the following style link to reference one of the other code themes available in the referenced `highlightjs\styles` folder:

```html
<link href="{$themePath}..\scripts\highlightjs\styles\vscodedark.css" rel="stylesheet" />
```

The default code theme used is `twilight`. Other code themes include `github`, `vs2015` (dark), `vs` (light), `monokai` (dark) and many more. Check the `PreviewThemes\scripts\highlightjs\styles` folder for more code themes.

Note that Preview Themes explicitly declare a Syntax Highlight Theme so if you create a custom theme you can specifically match a Syntax Highlight Theme to your custom theme.

#### Override Code Block Styling
In addition to replacing the Code Block theme, you can also add and override individual styles using the `Theme.css`  (or inline `<style>` in `Theme.html`) to override existing styles from a Code block theme. 

For example to change the background color of the code block rendering you could do:

```css
.hljs {
  background: DarkGreen !important;
}
```

> If you use the `Theme.css` style sheet you need to use `!important` to override settings due to the ordering of the code block theme after the main styles or you can re-arrange the order in `Theme.css`.

### Script Interaction and the `previewUpdated` Event
You can also add JavaScript code to the template to dynamically inject elements into the page to perform custom fixups of the document in the preview. 

One thing of note with this approach is the MM updates the page rendered as you type, so they page is constantly repainted and as a result you need to handle a specific `previewUpdated` event to run your script.

To demonstrate, I recently got a request for displaying Image titles below an image. So with an image tag like this:

```markdown
![Markdown Monster](https://markdownmonster.west-wind.com/Images/MarkdownMonsterLogo.jpg)
```

the **Markdown Monster** text should display below the image. To do this I added  script code to the `Theme.html` page just above the `</body>` tag:

```html
<script>
// hookup event
document.addEventListener("previewUpdated",figureTitles);

function figureTitles() {
  // loop through all images
  $("img").each( function() {
      var $img = $(this);
      var title = $img.attr("alt");
      
      // if alt title is found add it after the image
      if (title)
         $img.after("<p><small><b>" + title + "</b></small></p>")
 });
}
figureTitles();
</script>
</body> 
```

### Make the Preview your Own!
The concepts for customization is meant to be really easy to customize. You can start with an existing theme and tweak it, or go to town and create a completely new layout and theme for your Preview.