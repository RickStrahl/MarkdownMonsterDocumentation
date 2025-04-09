Markdown Monster allows you customize each of the main user interface components with:

* Application Themes
* Editor Themes
* Preview Themes

### Application Themes
The Application Theme controls the overall application coloring for windows, menus, controls and general application chrome. There are only two Application themes to choose from:

* **Dark**
* **Light**.

Here's the Dark Theme:

![](/images/darktheme.png)

And here is the Light Theme:

![](/images/lighttheme.png)

> #### @icon-info-circle Application Theme does not change Editor Theme
> Switching the Application theme does not affect the Editor's theming - change the Editor theme separately.

The Application Theme is set in **Tools->Settings**  with the `ApplicationTheme` key:

```json
"ApplicationTheme": "Dark"
```

> #### @icon-info-circle Restart required
> Making a change to the Application theme requires a restart of Markdown Monster. Although many theme changes are applied immediately some top level changes require a full restart.

### Editor Themes
Editor themes customize the editor and its syntax highlighting for your Markdown text. There are a number of light and dark themes available to use, using common TextMate style editor syntax highlighting themes.

The default dark theme is **twilight** and another popular one is **monokai**. Commonly used light themes are **visualstudio**, **github** and **textmate**.

![](/images/EditorPreviewThemeUi.png)

You can also set the theme in **Tools->Settings**:

```json
"EditorTheme": "twilight"
```

### Preview Themes
Preview themes are used in the HTML preview pane to format the rendered HTML output. Markdown Monster ships with a handful of preview themes: **Darkhan**, **Github**, **Medium**, **Blackout** and **Hipster**. You can easily create themes of your own by copying an existing theme or creating a brand new one based on plain HTML and CSS formats. 

![](https://github.com/RickStrahl/ImageDrop/raw/master/MarkdownMonster/PreviewThemes.gif)

Preview themes can be switched from the status bar or you can set the Preview Theme in **Tools->Settings**:

```json
"RenderTheme": "Github"
```

The default preview theme is **Github** which somewhat mimics Github's styling. Github styling includes some visual markers like a frame and large, fixed margins which is not ideal for rendering but it does match Github's styling. If you want a more responsive design, **Dharkan** is a simple design with similar layout characteristics as Github minus all the margins. If you're looking for a dark theme **Blackout** is your choice.

It's also easy to create custom themes - you can simply copy one of the existing themes and customize the relatively simple CSS. You can start with one of the existing themes and customize to your heart's delight.

To do this:

* On menu Tools | Open Preview Themes Folder
* This puts you in the current Theme folder
* Move up one folder level
* Copy any of the theme folders
* Create a new folder with the name for your new theme
* Make any changes to the CSS and HTML files

**Done!** You've created a new theme that now shows up on the list of themes in the editor based on the folder name.