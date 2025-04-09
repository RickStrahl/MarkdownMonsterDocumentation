Admonitions renders styled note/alert/warning boxes for content using an easy to use syntax:

```markdown
# Admonitions

:::note

This is an interactive **note** with a [link home](https://markdownmonster.west-wind.com)

:::



:::tip

This is a **tip**. Contained content can contain it's own markdown content

:::

:::info

Some simple information.

This has multiple paragraphs of text.

:::

:::warning

Some **content** with _Markdown_ `syntax`. Check [this `api`](#).

:::

:::danger

This is Dangerous!

:::
```

The above renders like this *<small>(styling will vary depending on the active Preview Theme)</small>*:

![](/images/AdmonitionsExtension.png)

### Enabling Admonitions
The Admonitions Render Extension is enabled by default using the **Tools -> Settings -> Use Admonitions** options in the configuration editor, via this setting in `MarkdownMonster.:

```json
{
    Markdown:  {
        "UseAdmonitions": true
    }
}
```

### Styling
Admonitions styling is handled via the[ Preview Theming styles in Theme.css](VFPS://Topic/_4NN17BFIC) for each preview theme.

The relevant sections in `Theme.css` are:

```css
/* DocFx Styles*/
.CAUTION, .IMPORTANT, .INFO, .INFORMATION, .ERROR, .TIP, .NOTE, .WARNING, .DANGER {
    padding: 0.1px 20px;
    margin: 15px 0;
    border-radius: 4px;
}

.CAUTION, .ERROR, .DANGER {
    border-left: 4px solid #cf222e;
}

    .CAUTION > h5, .ERROR > h5, .DANGER > h5 {
        color: #cf222e;
    }

    .CAUTION h5:before, .ERROR h5:before, .DANGER h5:before {
        content: "\f06a";
        font-family: 'Font Awesome 6 Pro';
        font-weight: 400;
        padding-right: 6px;
    }

.IMPORTANT {
    border-left: 4px solid #8250df;
}

    .IMPORTANT > h5 {
        color: #8250df
    }

    .IMPORTANT h5:before {
        content: "\f4a5";
        font-family: 'Font Awesome 6 Pro';
        font-weight: 400;
        padding-right: 6px;
    }

.WARNING {
    border-left: 4px solid #bf8700;
}

    .WARNING > h5 {
        color: #9a6700;
    }

    .WARNING h5:before {
        content: "\f071";
        font-family: 'Font Awesome 6 Pro';
        font-weight: 400;
        padding-right: 6px;
    }

.TIP {
    border-left: 4px solid #1a7f37;
}

    .TIP > h5 {
        color: #1a7f37;
    }

    .TIP h5:before {
        content: "\f0eb";
        font-family: 'Font Awesome 6 Pro';
        font-weight: 400;
        padding-right: 6px;
    }

.NOTE {
    border-left: 4px solid #0969da;
}

    .NOTE > h5 {
        color: #0969da;
    }

    .NOTE h5:before {
        content: "\f05a";
        font-family: 'Font Awesome 6 Pro';
        font-weight: 400;
        padding-right: 6px;
    }

.INFO h5, .INFORMATION h5 {
    color: #555;
}

.INFO, .INFORMATION {
    border-left: 4px solid #999;
}

    .INFO h5:before, .INFORMATION h5:before {
        content: "\f05a";
        font-family: 'Font Awesome 6 Pro';
        font-weight: 400;
        padding-right: 6px;
    }

```

You can customize these styles as needed. 

> ##### @icon-info-circle Create a new Theme for Changes
> Remember that if you make changes to any theme to save the theme in a new folder as existing Themes are updated with each Markdown Monster update.
> 
> [More info...](VFPS://Topic/_4NN17BFIC)