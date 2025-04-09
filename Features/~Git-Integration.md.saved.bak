Markdown Monster includes a number of helpful Git Integration features:

* Shows Git Status in the [Folder Browser](VFPS://Topic/_4WU1CJYKA)
* Commit and push the active doc or all pending changes
* Undo Changes
* Ignore Files
* Open your preferred Git Client
* Use your preferred Diff tool
* Push and Pull from Origin
* Clone a Git Repository
* Create a Git Repository
* Add local repository to Remote

Here's a what some of the main Git integration features look like:

![](/images/gitintegration.png)

> #### @icon-warning Git has to be Installed and Configured
> In order for Git remote operations to work in Markdown Monster, Git and the Git Credential Manager for Windows (part of Git install) have to be installed and globally accessible via `git.exe`. You can download and install Git from <a href="https://git-scm.com/download/win" target="top">this link</a>. You can also find a list of <a href="https://git-scm.com/download/gui/windows" target="top">GUI Git clients</a>.


## Committing the current Document to Git
If you already have a Git Repository configured and connected to a remote you can use the **Commit to Git** feature which is available in a number of places:

* On the Active Document tab's Context Menu
* In the Folder Browser's Context Menu
* In **File -> Git -> Commit to Git**
* Using the **alt-t-g** shortcut in the Active Document

![](/images/tabcontextmenu.png)

## Commit to Git Dialog
The **Commit to Git** menu gets you to the Commit Dialog shown in the first image above. The dialog display a list of pending changes that can be committed to Git. By default only the active file from the editor or the folder browser is selected in the list to make it easy to selectively update just the file you are currently working on.

You can optionally select other or all pending changes and commit those as well.

You can either **Commit** changes which commits to the local Git repository, or if the repository is connected to a remote like GitHub, BitBucket or VSTS, you can also **Commit and Push** which performs both operations in a single step.

> #### @icon-info-circle Quick Commit Shortcut
> If you only commit the currently active file that's pre-selected, you can quickly commit the form by pressing **ctrl-enter**. The shortcut behavior uses the **bold** tool button, which is remembered based on your last commit operation. 


You can also optionally **Ignore** files that are pending by right clicking and using the **Ignore File** option which adds it to the Git .gitignore. Note that this only supports explicitly ignoring the file by its full name. For wildcard ignore operations you need to use a dedicated Git client.

### Open external Diff Tool
You can also open an external Diff tool to compare changes between the current content of the file and the content that has been previously committed to Git.

To get to this feature:

* Use the file Context menu - Open in external Diff Viewer
* Double click file

By default MM recognizes the following Diff tools:

* Beyond Compare
* Meld
* KDiff

Or you can point at a custom Diff tool in:

```json
"GitDiffExecutable": "C:\\Program Files\\Beyond Compare 4\\BCompare.exe"
```

### Pull from Origin
The Commit Dialog includes an option to pull changes from the remote repository. The Pull operation pulls only from the **origin** default branch and performs a **merge commit** if successful.

For merge conflicts you can open the file with your specified Merge tool, or - more likely - open your external Git Client tool.

### Push to Origin
You shouldn't have to push explicitly often since you can **Commit & Push** but if you do need to explicitly submit previously committed changes when there are no pending files, you can just use **Push**.

### Open External Git Client
The Git features in Markdown Monster provide common use cases that you use with simple document management - it's not meant to be a full replacement for a full Git client.

For this reason you can optionally defer more complex tasks to your **preferred Git Client**.  A few popular ones that MM auto-detects are:

* [SmartGit](https://www.syntevo.com/smartgit/) (commercial)
* [Github for Windows](https://desktop.github.com/)
* [SourceTree](https://www.sourcetreeapp.com/)
* [GitKraken](https://www.gitkraken.com/)


An **Open in Git Client** menu option is available in all places where you also see **Commit to Git** and you can also jump to your Git client from the **Git Commit Dialog**.

The Git Client is configured in the `GitClientExecutable` key in **Tools -> Settings**:

```json
"GitClientExecutable": "C:\\Program Files (x86)\\SmartGit\\bin\\SmartGit64.exe",
```

## Folder Browser Git Commit
The folder browser displays change status icons for files, if the folder is part of a Git repository.

![](/images/folderbrowser_gitcommit.png)

You can also commit files from the Folder Browser by pressing `ctrl-g` in the file folder listing, or by using the context menu and **Commit to Git**. You can also undo changes to changed files which reverts back to the last committed change.

## Clone a Repository
You can also clone a repository from a remote site. To access this feature use **File -> Git -> Clone Repository** which brings you to this dialog:

![](/images/gitclonerepository.png)

The Git Repository URL is aware of the clipboard, so if you already have a URL on the clipboard it'll be pre-filled.

The Repository URL accepts a fully qualified Git Clone url which you can get from most Git repositories by clicking on the Clone URL. It also supports special handling for GitHub, BitBucket and VSTS repositories which allows for the base Web site url of the repository.

## Create a Repository
It's also possible to create a new repository for a folder directly in Markdown Monster:

![](/images/gitcreaterepository.png)

Simply specify a folder where you want to create your repository. 

> If the folder already has a Git repository a dialog, you'll get a warning in the status bar and you won't be able to create the repository. If you want to create a fresh repo in that folder, delete the `.git` folder, then try the create again.

## Add Remote to Repository
In some cases you may also want to attach a local repository to a newly created repository on a Remote. This typically works only if you already have a local repository and then create a new empty remote repository that you want to hook the existing repository to.

![](/images/gitaddremote.png)

Note adding a remote to an existing unsynched remote Git repository can have undesired effects. The typical use case is to attach the current repository to a new empty repository and then push. For almost all other scenarios cloning/forking is usually a better approach.

### Remote Configuration and Authentication
If you're connecting to a private repository you might have to use an external tool to connect to the remote and configure your credentials. Markdown Monster will in most cases prompt for credentials via a sign in dialog, but there are cases where this may not work. In that situation you may have to ensure you can access the remote repository **externally** using the Git Command line, or another tool like [Github Desktop](https://desktop.github.com/), [SmartGit](https://www.syntevo.com/smartgit/), [SourceTree](https://www.sourcetreeapp.com/), [GitKraken](https://www.gitkraken.com/) or similar, which provide more robust credential configuration support than Markdown Monster internally.

Once authentication is configured and you can push and pull either from the command line or using above tools, you can then also use Markdown Monster's Git remote features.

### Setting up Git Credential Helper on Windows
One thing that can help with authentication configuration is using the Git Credentials Helper:

```ps
git config --global credential.helper manager
git config --system credential.helper manager
```

This configures Git in such a way that you get the pop up authentication dialog for Git providers, and once credentials have been successfully applied they are cached and reused on subsequent requests.

Here's more info on the Git Credential Manager for Windows (built into Git) and what it does:

* [Git Credential Manager for Windows](https://github.com/microsoft/Git-Credential-Manager-for-Windows)