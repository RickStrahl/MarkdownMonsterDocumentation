Markdown Monster is essentially a text editor and so supports only fixed width, monospaced fonts.

On Windows the most common monospaced font is **Consolas** which is also the default font that is set in Markdown Monster. 

You can change the font, font-size and line height in the Markdown Monster settings via **Tools->Settings**:

```json
{
    ...
    "Editor": {
        "Font": "Consolas",
        "FontSize": 17,
        "LineHeight": 1.3
    }    
}
```

The font-size is in pixels and the line-height determines the spacing between lines. The larger the line-height the more space there is between lines of text.

> #### @icon-warning Don't use Proportional Fonts
> Note that while you can set a non-monospace font, this will cause the editor to not properly track the cursor rendering the editor nearly unusable. Markdown Monster doesn't support that scenario, so please make sure you choose a monospace font.


### Some Nice Installable Monospace Fonts

* <a href="https://github.com/i-tu/Hasklig" target="top">Hasklig</a>
* <a href="https://github.com/tonsky/FiraCode" target="top">Fira Code</a>
* <a href="https://www.fontsquirrel.com/fonts/dejavu-sans-mono" target="top">Deja Vu Mono</a>
* <a href="https://www.dafont.com/monofur.font" target="top">MonoFour</a>