Markdown Monster has limited support for making an initial post to Medium Publications. Support is limited due to the limitations of the Medium API as you can only make a **one time post** to the  [Medium API](https://github.com/Medium/medium-api-docs). There's no support for editing or retrieving posts. Once an initial post was made you have to edit and manage the *'story'* on the Medium Web site.

This still provides a lot of utility as you can do the bulk of article creation and content embedding in Markdown Monster and only do your editing in the online editor. You just want to try and do as much editing and cleanup **before you post to Medium** to avoid having to use the online editor.

### Medium Preview Theme
Markdown Monster includes a **Medium Preview Theme** you can select while editing Medium posts, to get a preview experience that's a closer to a default Medium Web site. Of course you are not required to use that theme, it's provided merely as a convenience to those that use the default theme.

To select the them use the **Status Bar Preview Theme selection dropdown** on the bottom right and select `Medium` as the Preview Theme.

### Source Code Formatting Limitations
Medium has no support for syntax coloring or code formatting in its default themes so any code snippets you post are posted as plan, non-syntax colored formatted text blocks. 

Although you can post source code and it will show as plain formatted text, if you want better source code formatting you have to use embedded code snippets like snippets from Gist for example. You can use the Paste Code as Gist Addin to provide formatted code.

Here's a screen shot that demonstrates a post in MM and then pushed to Medium:

![](///images/MediumMMSideBySide.jpg)

### Configuration for Medium
Configuration for a Medium Weblog looks like this:

![](///images/MediumConfiguration.png)

> In order to publish to Medium you need to ensure you have at least one **Publication** active in your Medium account.

To set up a new Medium Account follow these steps:

* Set the **Weblog Type to Medium**
* Enter the Access Token using an **Medium Integration Token**
* Then click the down button on the **Weblog Id or Publication** dropdown
* Pick your **Medium Publication** to publish to
* A publication ID will be shown in the drop down.

### Getting a Medium Integration Token
For security Medium requires that you use a Medium issued integration token. You can generate a token from the [Medium Settings page](https://medium.com/me/settings). 

To create a Medium Integration Token:

* **Log in** to your Medium Account
* Click on your **User account icon**
* Click **Settings**
* Scroll to **Integration Tokens**
* Enter a description for the token
* Click **Get Integration Token**
* **Copy the generated token** to the clipboard
* **Paste the token** into the **Access Token** field in Weblog Configuration 

If you're already logged into your Medium account, here's the direct link to the page:  
https://medium.com/me/settings

### Publishing to Medium
The Medium API is extremely limited and has no support for any extended features. Basically, the only thing that the client can send is the actual HTML and images, and tags. 

Abstracts and Categories are ignored, so those fields are not available when publishing to Medium.

And please remember, unlike other Weblog types:

> Medium publishing is a one time operation - editing is not supported through the Medium API due to forced limitations of the Medium public API.

### Limited but still Useful
Although frustrating the limited Medium API support, being able to get an initial post to Medium is still very useful especially if you do a good job of editing your posts before you finalize our post and publish it to Medium for public sharing.