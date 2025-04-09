Markdown Monster can be downloaded and evaluated for free, but a license <a href="https://markdownmonster.west-wind.com/pricing.aspx" target="top">must be purchased for continued use</a>. Licenses are per user, rather than per machine, so a licensed user can use Markdown Monster on as many computers as needed. Various license packs and an organizational license are also available to use Markdown Monster for an unlimited number of installations within a single organization. 

Licenses are valid for the major version for which it was purchased such as v1.0 to v1.99.

For pricing and purchasing of a license please check this link:

* [Markdown Monster Pricing and Purchases](https://markdownmonster.west-wind.com/pricing.aspx)

### Registering 
Purchases provide you with a Registration Key that you can apply to a Markdown Monster installation. To register your instance of Markdown Monster:

* Open Markdown Monster
* Go to **Help -> Software Registration**
* Enter your Registration Key into the text box

Here's what the registration form looks like:

![](/images/RegistrationForm.png)

Once registered the **(Unregistered)** header disappears from the toolbar and all of the registration reminder dialog popups no longer pop up.

> #### @icon-info-circle Each Machine Requires Registration
> If you install Markdown Monster on multiple machines, each machine requires its own registration - registrations are never shared across machines due to the machine specific registration key **even if you share configuration settings**. 

### Registration Checks
Due to the high volume of fraudulent license attempts Markdown Monster now validates licenses occasionally. In order to validate a license **an Internet Connection is required**. Licenses are checked once a week, and if not online are flagged for removal if the next online license check fails as well. 

Once a license is removed Markdown Monster reverts back to **Unregistered** mode with registration reminders and some advanced features disabled. To restore the license, you have to re-enter your license information in the registration form.

> We realize that this may cause an occasional un-registration of a valid license, but with registration rates running close to 1-100 with registered vs. fake registrations we needed a mechanism to disallow bypassing the registration check mechanism. 

### Key Storage
When Markdown Monster is registered it registers the current instance with a machine specific key that is stored in one of two locations on your local hard drive as `Registered.key`

* In the Markdown Monster Install Folder (`%localappdata%\Markdown Monster` by default)
* In the Markdown Monster Common Folder (`%appdata\Markdown Monster` by default)

The preferred location is the Install folder because it doesn't sync or is backed up with other configuration settings. Since the registration is machine specific `Register.key` **cannot be used on multiple machines**. Each machine requires it's own registration `Register.key` file.

The local install location is used **if permissions allow writing the `Register.key` file there**. If not the `CommonFolder` location is used which by default is in `%appdata%\Markdown Monster` but can be [user defined](VFPS://Topic/_4X314391I) including shared locations like DropBox or OneDrive.

> If you run Markdown Monster in development mode or you have multiple instances it might be useful to put `Register.key` explicitly into the `%appdata\MarkdownMonster` folder as that location is shared for all instances across the same machine. Otherwise each instance needs its own registration key in the appropriate startup directory.

### Shared Configuration with DropBox and OneDrive etc.
If you're using DropBox or OneDrive to share configuration make sure that you register each machine separately and you store the registration key explicitly in the Markdown Monster install folder. If MM can't write due to permissions, you can explicitly move the `Register.key` file from your common files location to the install location with temporary admin rights.