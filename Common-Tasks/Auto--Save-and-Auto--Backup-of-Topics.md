Markdown Monster supports both **Auto-Save** and **Auto-Backup** features. Only one of these is active at any time with Auto-Save taking priority if set. Auto-Backup is enabled by default.

![](/images/AutoSaveAutoBackup.png)

### Auto-Save
You can configure Markdown Monster **to automatically save your Markdown files as you type**, so the file is **immediately saved** after a 1 second idle delay. As soon as you stop typing for more than 1 second the file is updated.

> **Untitled** documents are not saved until you save them to a permanent location on disk.

This setting is controlled via the `AutoSaveDocuments` setting and the setting is `false` by default.

```json
"AutoSaveDocuments": true,
```

### Auto-Backup
Auto-Backup backs up typed content as you are typing. Backups are saved in a `youFile.md.saved.bak` backup file format. Whenever you save or close the file in the editor, the backup file is deleted.

The backup file is used to ensure that if Markdown Monster closes unexpectedly, that your unsaved content will be available to you when you return.

If a backup file is found when Markdown Monster opens or re-opens a file, it'll show the `*.md.saved.bak` file next to the opened file. You can then compare the two files and copy the content out of the backup file into the primary file as needed.

This feature is controlled via the `AutoSaveBackups` configuration setting in **Tools -> Settings** or in the configuration file:

```json
"AutoSaveBackups": true,
```  

> #### @icon-info-circle Backup Files don't show in the Folder Browser by Default
> The Folder Browser by default excludes `.md.saved.bak` files, so the backup files are not visible as they can add a lot of noise to a folder listing. If you want to see or access the file, you can toggle the **Show All Files** toolbar button in the Folder Browser's toolbar, or open the folder in Explorer.

> #### @icon-info-circle Backup Files and Git
>Markdown Monster saves the recovery file in the same folder as the original document with the `md.saved.bak` extension. This is necessary so that the recovery file can be found on re-opening in the future to potentially capture any lost data.  
>
> The side effect of this process is that there's a `.saved.bak` file floating around whenever Markdown Monster is editing text. If you are using Git this may interfere with your GIT commit as the backup file shows up as file that has changed.
>
>The easiest way to fix this is to add the `*.bak` or `*.saved.bak` to your `.gitignore` file for your project (or global `.gitignore`). Add one of the following to your `.gitignore` file:
> ```
> *.bak
> *.saved.bak
>```