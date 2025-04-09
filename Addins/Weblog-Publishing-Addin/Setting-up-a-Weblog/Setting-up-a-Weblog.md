The first thing you need to do is set up one or more Web sites for your blog. In order to publish to the Weblog your blog has to support:

* **[WordPress API (classic)](VFPS://Topic/_4UW00NUIZ)**  
This API is used by any WordPress blog. MM accesses WordPress via the old XmlRpc API since we only use basic features for posting and retrieving posts. This API uses a common endpoint (usually **XmlRpc.php**) and username and password authentication to send requests.

* **[MetaWebLog API](VFPS://Topic/_4UW00NUIZ)**   
This API is commonly supported by 3rd party Weblog engines. Functionally it's very similar to WordPress's core API as it uses the same base XmlRpc structures. It uses username and password authentication with each request, but unlike WordPress, the endpoint URL is different for each configuration. 

* **[Medium](VFPS://Topic/_4UW03TMCU)**  
Medium is a popular online blogging platform and Medium provides its own **very limited API** that only allows for **one time posting** of new *Stories* (posts). The [Medium API](https://github.com/Medium/medium-api-docs) has no support for re-posting, downloading or even loading existing posts. Still initial publishing support is very useful for getting initial content to Medium.

* **[Jekyll Local Folder Publishing](VFPS://Topic/_5RV00RX4I)**  
Jekyll is a popular static site generator used on Github and it has support for hosting Weblogs. This mechanism is a local file publishing mechanism that publishes a MM Weblog Post into the Jekyll folder structure copying both the Markdown content as well as the associated assets. It can optionally also build the Jekyll site and preview content.

### Add, Edit, Delete Weblogs
The Weblogs Tab allows you to create, edit and delete multiple Weblogs that you want to publish to. 

![](//images/CreateEditWebLog.png)

For each blog you need to provide a Blog name, a Blog ID (some identifier the blog engine provides), an Endpoint URL where requests are received, and either a username and password, or access token to authenticate requests.

### Adding a new Weblog
To create a new Weblog entry:

* Click on the @icon-rss icon on the toolbar
* Go to the Web Logs tab
* Click New
* Fill out the form


The form is going to look slightly different depending on the blog type. MetaWeblog and Wordpress will have username and password inputs, while Medium has an API token instead.

### Configuration Fields

##### Name
This is the display name for the blog you see in the dropdown for blog selection.

##### Blog Id / Publication Id
Blogs have a blog Id or Publication Id associated with them. This is primarily used for blog engines that host many blogs, but even single site blogs use this value. If you know this value you can type it into the textbox.

The dropdown button attempts to download available blogs/publications and lets you interactively choose from a list **if your Blog engine supports it**.

> In order to look up blogs make sure username/password or the access token and Api Url fields are set first. Otherwise you can't connect to the API to get this data.

##### Api Endpoint Url
This is the most important value, which holds the API endpoint URL which responds to requests. If you know the full endpoint URL to the API - great, just type it in. 

To auto-discover the Endpoint URL enter your Weblog's home page Url and click on the @icon-gear button to test or discover your endpoint URL. This button attempts to discover the endpoint Url. When it's done it displays its result on the status bar of the window.

Most public blog engines support **RSD (Real Simple Discovery)** which lets Markdown Monster discover the actual API Endpoint. If RSD is supported by your Blog engine, it retrieves the **Api Url** and **BlogId** and fill those values for you. Yay!

If the endpoint search fails, you have to figure out your API endpoint. If you're currently using third party software to publish posts, check the documentation to see what URL is used to send API requests.

##### Blog Type
Determines what type your blog is. This is important for MM to know how API requests need to be processed as each type uses a different API.

##### Username/Password
Wordpress and MetaWeblog API require username and password to connect to the API service. This value is sent on every request.

The username and password are stored in encrypted form in the configuration using machine specific encryption keys.

> **Important**: Username and password are sent with each request, so make sure you use SSL (https://) requests to your server to encrypt request data sent to the server.

##### Access Token
Medium uses a User Access Token to validate users. 

To get a User Access token for Medium:
* Log into Medium
* Click on your Profile Picture
* Click on Settings
* Scroll down to Integration Tokens
* Enter a name for your Token
* Click on *Get integration token*
* Copy the integration token
* Paste into the Access Token field of the Weblog Configuration form
* 
The access token is stored in encrypted form in the configuration using machine specific encryption keys.

### More info on providing your Weblog API Endpoint
In order to access a Weblog and post new and updated posts to the Weblog, you have to provide

* Blog Type (Wordpress or MetaWeblogApi)
* An API Endpoint Url
* A username and password

### The Weblog API Endpoint Url
The key item on this page is the **Api Url** which is the final endpoint where the API listens for incoming API requests. 

If you know that final obscure Endpoint Url for your Weblog API- awesome, you're done! 

For the rest of us a little help is needed.

### Discovering the Weblog API Endpoint Url
To discover the Endpoint URL, rather than putting in an Endpoint URL, enter your Weblog's home page Url and click on the @icon-gear button to test or discover your endpoint URL. This button goes out and tries to discover the endpoint Url. When it's done it displays its result on the status bar of the window.

Most public blog engines support **RSD (Real Simple Discovery)** which lets Markdown Monster discover the actual API Endpoint. If RSD is supported by your Blog engine, it will retrieve the **Api Url** and **BlogId** and fill those values for you. You're left with username and password to fill out.

If the endpoint search fails, you will have to figure out your API endpoint. If you're currently using some other software to publish posts, check there to see what URL is used to send API requests or use a tool like Fiddler to via the API traffic and see what the URL is where Weblog API requests are made.