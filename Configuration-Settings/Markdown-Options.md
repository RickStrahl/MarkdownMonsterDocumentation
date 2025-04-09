#### AutoLinks
Determines whether URLs are automatically turned into links. `true`

#### Abbreviations
Determines whether common abbreviations are expanded. `false`

#### StripYamlFrontMatter
Strips Yaml FrontMatter from any Markdown content. `true`

#### EmojiAndSmiley
Interprets common emoji and smiley characters like `:smile:` or `:-)` and turns it into Emoji. `true`

#### ListExtras
Provides features like Github Check lists and nested lists: `true`

#### Figures 
Allows for figure referencing in a location other than the current location. true

#### GithubTaskLists
Allows for Github checkable task lists by using `[ ]` and `[x]`.

#### SmartyPants
Converts common typographic characters to proper typographic publishing settings. Quotes to curly quotes dashes to em dashes etc. Use for print publishing of literature - leave off for technical content. `false`

#### Diagrams
Support for Mermaid markup. Note the MM preview doesn't support Mermaid, but the renderer produces it and you can preview in the external browser.

#### RenderLinksAsExternal
Renders all links with a target="_blank" to force links to be externally opened in a new tab/window. Useful in some documentation scenarios where you don't want to lose your place in the document. `false`

#### AllowRenderScriptTags
By default script tags are stripped from Markdown content. Set to true if you need to explicitly run scripts as part of your markdown for things like embedded Gists for example. `false`

#### MarkdownParserName
This is the name of the Markdown Parser used. MM ships with `MarkDig` which is the default parser, but addins can add additional parsers which are selectable from the dropdown on the status bar. `Markdown`

#### GenericAttributes
Allows attaching generic HTML attributes to the active 'element'. Example: `{ class='error-message' id="MyHeader"}` using explicit attributes or using CSS Selector style syntax `{ .error-message #MyHeader }`. The attributes are  appended to the generated HTML element on the same line (ie. header, list item, paragraph etc.). 
[more info](https://github.com/lunet-io/markdig/blob/master/src/Markdig.Tests/Specs/GenericAttributesSpecs.md)

#### CustomContainers
Allows wrapping a Markdown element or element group with a container element. Using a block like `:::note` and `:::` to denote a block will generate a `<div class="note"></div>` around the Markdown block it surrounds.
 
#### ParseDocFx
If set parses several common DocFx 'commands' like file inclusion, link expansion and a few others.
 
#### MarkdigExtensions
Allows you to explicitly specify MarkDig extensions to load. MM loads a default set, but you can modify this list which allows you to add custom extensions.
`emphasisextras,pipetables,gridtables,footers,footnotes,citations,attributes`