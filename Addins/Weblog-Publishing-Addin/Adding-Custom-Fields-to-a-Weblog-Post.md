The Weblog Publishing addin supports custom fields when publishing posts to MetaWeblog API and WordPress blogs, using the **CustomFields** extensions to these two APIs.

You can edit CustomFields as part of the Weblog Post Form which includes a section to add a key name and value for any custom fields you want to send to the server.

![](//images/CustomFields.png)

Use the @icon-plus-circle icon to add a new Custom Field to the list and @icon-remove icon to remove the **selected** custom field from the list.

You can edit the custom field entries in the list. Changes are saved when you **Post to Weblog** or **Save Metadata**.

### CustomField Meta Data
CustomFields data is stored as part of the Meta Data associated with a post, which is created when you either **Post to Weblog** or **Save Metadata**. This adds the meta data YAML to the beginning of the post:

```yaml
---
title: IIS and ASP.NET Core Rewrite Rules for Static Files and Html 5 Routing
abstract: If...
keywords: Static Content, Html 5 Routes, IIS Rewrite, Angular, Kestrel, IIS, ASP.NET
categories: ASP.NET Core, IIS
weblogName: West Wind Web Log
postId: 220994
customFields:
  mt_publishon:
    key: mt_publishon
    value: 05/10/2017 08:00
  mt_location:
    key: mt_location
    value: Hood River, OR
---
```

> #### customFields Yaml Format: Object Collection
> Note that the **customFields** structure is a bit more complex than just a key value pair, as there is an additional Id field that might have to be stored as part of a post. The **customFields** key is followed by a list of keys with an object that has **key**, **value** and **id** fields.