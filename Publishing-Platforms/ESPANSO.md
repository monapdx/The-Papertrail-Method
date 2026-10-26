While not a publishing platform, Espanso is a powerful text expander that can do everything from text replacement to running scripts for you.

One of the more clever ways to use it for The Papertrail Method is to create a trigger using something like :submit to create a form that pops up with the fields you need for submissions. 

You then fill out the details and hit submit, and it can do...well, pretty much anything with that data. 

One way to use the form data is to have Espanso automatically generate markdown or HTML using the templates we included in the Github section.

For example, typing the colon followed immediately by paul will generate this:


````
|              |                                                                  |
| ------------ | ---------------------------------------------------------------- |
| **From:**    | Paul Emerson, Executive Producer `<paul@themisogynypodcast.com>` |
| **To:**      | Derek Vale, Host, `<derek@themisogynypodcast.com>`               |
| **Subject:** | Fwd:                                                             |

```text
Your submitted message will be inserted here.
```

-Paul Emerson  
**Executive Producer**  
*The Misogyny Podcast*
````

This makes manually editing the markdown completely unnecessary. 

You can create a trigger in Espanso for every character in your fictional organization and your broader story, then have it automatically generate an email sent by them to another character or to the organization.

Triggers in Espanso look like this:

`:trigger` 

They are written in YAML and once you've installed it on a Windows machine, you can find its folder using the following path:

`"C:\Users\Admin\AppData\Roaming\espanso"`

Inside you should find two folders:

- config/
- match/

Open the match folder and you'll find a file with the name:

`base.yml`

Open it up in Notepad++ or another text editor to add new triggers and see your existing ones.

You don't have to store all of them in base.yml if you don't want to.

Just create a new file in the match folder and name it whatever you want.

papertrail.yml
characters.yml
emails.yml

Anything works. 

Here is a 

Here is a [Python script](https://drive.google.com/file/d/1lfEanCgfIer3OUDm6eA31qtoOLV1IT7D/view?usp=drive_link) I created that you can drop into your match folder, along with a [.BAT script](https://drive.google.com/file/d/1n9JixLDwMxBcN8de4QqBpd__sOYlUXco/view?usp=drive_link) that will automatically generate you a markdown file that lists all your Espanso triggers from base.yml.

Each time you add new triggers to base.yml, double click the .BAT script and it will regenerate your markdown table and add the new triggers.

The third column of the markdown table is left blank for your short description of what the trigger does. You can regenerate the table without losing your manually added descriptions, but the rest of the table values will update each time you run triggers.bat.

Here is an example of what the scripts will generate:

[espanso-shortcuts.md](https://drive.google.com/file/d/193IBNdvymAU0U0B64R0QJk0sLrNskgD5/view?usp=drive_link)




