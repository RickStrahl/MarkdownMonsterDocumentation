Markdown Monster can easily embed FontAwesome icons into your Markdown text. If your target site's styles load FontAwesome you can take advantage of MM's simplified FontAwesome embedding.

To add a FontAwesome Icon simply use the **&#64; icon-iconName** shortcut to embed the icon. For example, the following adds FontAwesome's round circle info icon into the text below:

```markdown
> #### @icon-info-circle Notice
> blah blah blah
```

which produces:

> #### @icon-info-circle Notice
> blah blah blah

Notice the icon info icon which is embedded by the **&#64; icon-info-circle** syntax, which is responsible for the embedded icon. 

Here's another example:

```markdown
Click on the @icn-camera icon to take a screen shot.
```

which produces:

<div class='well'>
Click on the @icon-camera icon to take a screen shot.
</div>

To insert a FontAwesome Icon, simple use **&#64; icon-** followed by the <a href="http://fontawesome.io/icons/http://fontawesome.io/icons/" target="top">FontAwesome Icon name</a> which you can find on the FontAwesome web site.
 
All of Markdown Monster's Preview styles include FontAwesome styles so the preview and exported documents will always include the FontAwesome icons.

### More sophisticated Icon Usage via HTML
You can also use more sophisticated icon displays, like rotations for example, but for those you have to use HTML markup:

```markdown
> #### <i class="fa fa-gear fa-spin fa-2x" style="color: firebrick"></i> Configuration
> Configuration can be launched from the **Tools -> Settings** menu option.
```

which produces: 

> #### <i class="fa fa-gear fa-spin fa-2x" style="color: firebrick"></i> Configuration
> Configuration can be launched from the **Tools -> Settings** menu option.

Icons are a great way for callouts or quote blocks, as they can make content more visually interesting. But don't overuse these icons and use them consistently on your sites and documentation.

> #### @icon-warning Requires FontAwesome on your Site
> It's important to understand that FontAwesome Icons only work if FontAwesome is loaded into the HTML page. Markdown Monster's preview themes all include FontAwesome on the preview page, but your target Web site or documentation may not include it, in which case the icons will not render. 
>
> Make sure that FontAwesome is available on your output target before using this feature.
