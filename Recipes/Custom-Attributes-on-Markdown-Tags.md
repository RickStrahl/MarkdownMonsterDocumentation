*How do I add custom styling or attributes to my Markdown Tags?*

> **Markdown natively doesn't support custom tags on rendered Markdown expressions.** 

Markdown is intended to be a very simple text based format and it relies on common, semantic styling to provide formatting for your rendered Markdown generated HTML output.

However, sometimes you need to explicitly override render behavior with custom styling or naming of elements. For example, it can be difficult to have a one size fits all image size that works both for large and small images, or perhaps you need to assign a linkable ID to a header or assign a custom class to bit of text.

There are two ways around the Markdown limitations to add custom attributes:

* [Use Raw HTML instead of Markdown ](#raw-html)
* [Use Generic Attributes](#generic-attributes)

> #### @icon-warning Make sure your Markdown Destination Supports these Feature
> Although these solutions exist and will render just fine in Markdown Monster, **they are not part of standard Markdown**! You have to **ensure that your final publishing target platform and the Markdown Parser used with it supports them**. 
>
> Markdown Monster's preview and parser (*MarkDig*) supports them and so the always preview works, but that's no guarantee it'll work on your target publishing platform. For example, GitHub which does not support either feature. *Check for support on your final Markdown platform before using these features.*

## Raw HTML
Markdown is a superset of HTML so you can actually use raw HTML inside of your Markdown documents. If your need for custom attributes or styling is rare, this is a reasonable option as it's easy enough to embed custom HTML into a Markdown document.

Here's an example:

```markdown
### Header
This is a custom
<a href="https://markdownmonster.west-wind.com" target="_blank" style="font-size: 1.1em">Web Site link</a> 
that is rendered as raw HTML.

<img src="image.png" style="width: 5rem" />

And on we go.
```

As you can see you can mix and match Markdown and HTML and it's possible to get quite creative with the Html. For example, you can wrap styled `<div>` tags around blocks of Markdown, add style and script blocks, in addition to simple attribute additions. There are some special rules about how Markdown works inside of HTML blocks - you want to leave blank lines between the HTML and markdown blocks  to separarate them - so you have to experiment a bit to see what works and what doesn't.

**Configuration Setting**  
Markdown Monster supports turning off raw HTML rendering as an option, but it is enabled by default. You can find it in the Settings Window under **No Html** in the Markdown section.

`Markdown.NoHtml": false`

## Generic Attributes
Generic Attributes is a common Markdown Extension that lets you add additional Html markup by adding `{...}` after a markdown element (ie. header, paragraph, image, link, code etc.). You can specify CSS directives like CSS Classes (prefixed by `.`) and ids (prefixed by `#`) or provide raw element attributes like `style` or `class` or anything else.

Here are some examples:

```markdown
# CSS Classes{.WARNING}
Using `.css-class` syntax lets you apply custom CSS classes.

## Id Values{#Updates}
Using `#id` lets you apply custom ID values.

## Custom Styling{style="color:darkgoldenrod"}
For everything else you can use attributes

## Miscellaneous examples
[West Wind WebSurge](https://websurge.com){title="WebSurge Stress Tester"}

![](https://markdownmonster.west-wind.com/Images/MarkdownMonster_Icon_256.png){style="width:50px"}
```

Here's what this renders like:

<style>
.render-block { background: #f9f9f9; padding: 1em; border-radius: 0.5em; }
</style>
<div class="render-block">

# CSS Classes{.WARNING}
Using `.css-class` syntax lets you apply custom CSS classes.

## Id Values{#Updates}
Using `#id` lets you apply custom ID values.

## Custom Styling{style="color:darkgoldenrod"}
For everything else you can use attributes

## Miscellaneous examples
[West Wind WebSurge](https://websurge.com){title="West Wind Web Surge Stress Tester"}

![](https://markdownmonster.west-wind.com/Images/MarkdownMonster_Icon_256.png){style="width:50px"}
</div>


**Configuration Setting**  
Markdown Monster supports turning off Generic Attributes as an option, but it is enabled by default. You can find it in the Settings Window under **Generic Attributes** in the Markdown section.

`Markdown.GenericAttributes: false`