Markdown Monster supports saving documents using encryption that protects files from prying eyes. When you save a document it's encrypted with a password of your choice and can then only be opened again by using that same password.

> Files are encrypted using two-way TripeDES Encryption.

### Encrypting a File
To encrypt a file:

* Open and edit your file as usual
* Use **File -> Save As Encrypted File**
* Pick a filename to save to
* Enter a password to encrypt the file with

![](/images/SaveAsEncrypted.png)

Once a file has been saved with encryption you have to use Markdown Monster to re-open it. Markdown Monster embeds a marker into the document that identifies the document as a encrypted document and then automatically prompts for a password when re-opened.

### Decrypting a File
To decrypt a file:

* Open the encrypted file
* Enter the password previously used to save the file

![](/images/DecryptFile.png)


> #### @icon-warning Important
> Once you encode a file with a password you have to use Markdown Monster to decode that file and open it again. 
>
> Also be sure to remember your password: You won't be able to open it **if you forget the password**. So please make sure you remember or properly store your password (hopefully in a password manager).