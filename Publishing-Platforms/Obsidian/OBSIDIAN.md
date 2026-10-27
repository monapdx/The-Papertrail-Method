

While Obsidian requires plugins to achieve the same types of functionality that Github offers natively when it comes to including forms and creating specific types of content based on submitting them, it's a great place for authoring episodes and creating the same fundamental folder structure as a Github repo.

The first plugin you should install to add powerful functionality is **[JS Engine](https://community.obsidian.md/plugins/js-engine)**.

Here is an example of an **[INBOX-FORM](INBOX-FORM.md)** for Obsidian that should work if you have the JS Engine plugin installed.

It's just got the basics: Email, Subject, Message.

It auto-detects existing folders in your Obsidian vault, and also has the option to create a new Inbox folder for storing submissions.

When you fill out the form and hit submit, a new note will be created in the folder you specified.

**The frontmatter properties for the note will include:** 

- Date submitted
- Value for the email field
- Value for the subject line

The actual note body will include the value for **Message**.

Folders can act as an email **[ACCOUNT](../../Content-Types/ACCOUNT.md)** with sub-folders for typical inbox conventions like SENT. 

