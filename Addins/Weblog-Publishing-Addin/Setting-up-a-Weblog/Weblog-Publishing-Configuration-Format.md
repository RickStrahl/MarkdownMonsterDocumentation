The Weblog Publishing feature is configured in the `WeblogAddin.json` configuration file in the `AppData` folder. You can just manually edit the file.

The easiest way to edit configuration settings is to:

* Click on the @icon-caret-down button next to the @icon-rss button in the toolbar
* Open `WeblogAddin.json` in an Editor (or Markdown Monster)
* Make changes to the file

The file looks something like this:

```json
{
  "PostsFolder": "C:\\Users\\rstrahl\\DropBox\\Markdown Monster Weblog Posts",
  "ReplacePostImagesWithOnlineUrls": false,
  "LastWeblogAccessed": "West Wind Web Log",
  "RenderLinksOpenExternal": true,
  "Weblogs": {
      "6b9hs6ni": {
      "Id": "6b9hs6ni",
      "Name": "West Wind Web Log",
      "Username": "rstrahl",
      "Password": "2g5k05dGevRDmoavkprq+A==*~~*",
      "AccessToken": null,
      "ApiUrl": "https://weblog.west-wind.com/weblogapi.ashx",
      "BlogId": "1",
      "Type": "MetaWeblogApi",
      "AuthenticationType": "UsernamePassword",
      "LaunchCommand": null,
      "PreviewUrl": null,
      "CustomFields": null
    },
    "rk7wof4b": {
      "Id": "rk7wof4b",
      "Name": "Rick Strahl WordPress",
      "Username": "rstrahl",
      "Password": "Figt\cS+UiTHSTyZowefrE9ahq+Smur4*~~*",
      "AccessToken": null,
      "ApiUrl": "https://rickstrahl.wordpress.com/xmlrpc.php",
      "BlogId": "635965",
      "Type": "Wordpress",
      "AuthenticationType": "UsernamePassword",
      "LaunchCommand": null,
      "PreviewUrl": null,
      "CustomFields": null
    },    
    "diidtj5c": {
      "Id": "diidtj5c",
      "Name": "Local Jekyll Blog",
      "ApiUrl": "C:\\projects\\Test\\jekyll\\myproject",
      "BlogId": "1",
      "Type": "LocalJekyll",
      "AuthenticationType": "UsernamePassword",
      "LaunchCommand": "c:\\windows\\SysNative\\bash.exe -c \"cd /mnt/c/projects/test/jekyll/help; bundle exec jekyll server\"",
      "PreviewUrl": "http://localhost:4000/{0}",
      "CustomFields": null
    }    
```

Values should be pretty self explanatory. The main configuration point is the default **PostsFolder** which determines where new posts are created by default. 


**ReplacePostImagesWithOnlineUrls** determines how links are embedded:

* Inline 
* As Reference Links

Reference links embed link Ids inline with a related image reference at the end of the document. Personally I find this reference linking very annoying as images easily break when you move them, but this has been a heavily requested feature, perhaps because a few places like StackOverflow use it.

Individual Web sites are configured in the list below, but it's easier to do this through the user interface, and you have to use that in order to hash  the password properly anyway.