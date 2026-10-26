To use The Papertrail Method using GitHub's native features is surprisingly easy and straightforward, you just need to map the conventions to the existing names that GitHub gives them.

For example, you'd first set up a GitHub repository and ideally name it using the name of your fictional **[ORGANIZATION](../Content-Types/ORGANIZATION.md)**. This repo acts as the backend of your show, news station, or podcast.

You can use GitHub Pages as the public-facing official website for your organization. Here is [an example](https://monapdx.github.io/The-Misogyny-Podcast/) of the one I made for my fictional podcast.

This is where you would link to each **[EPISODE](../Content-Types/EPISODE.md)** or other type of content in the **[PUBLICATION](../Content-Categories/PUBLICATION.md)** category.

Here is how the other parts of GitHub connect to the method:
```
REPOSITORY → ORGANIZATION’S WORKSPACE
ISSUE FORMS → SUBMISSION FORMS
ISSUE BODY → ORIGINAL SUBMISSION
ISSUE COMMENTS → EMAILS BETWEEN CHARACTERS
ISSUE + COMMENTS → THREAD
PROJECT → CORRESPONDENCE TRACKING
FILTERED PROJECT VIEWS → ACCOUNT INBOXES
LABELS → SUBMISSION TYPES

```

## GITHUB ISSUES & COMMENTS

Issue forms must be .yml (YAML) files that are located in the following folder in your GitHub repo: `.github/ISSUE_TEMPLATE/`

You can just include a general submission form if that's sufficient, or you can include several for different types of submissions.

For example, say that your organization is a radio station that hosts several different on-air segments and/or shows.

You could create Issue templates for each one.

It would look something like this:

`.github/ISSUE_TEMPLATE/`
 - morning-show.yml
 - song-requests.yml
 - call-ins.yml
 - contest-entry.yml

You act as the author behind each fictional identity: fill out forms on behalf of submitters, then write comments as the characters receiving and discussing their messages. The From and To fields identify the fictional participants, even when you write everything from a single GitHub account.

I made [this tool](https://monapdx.github.io/Github-Tools/issue-template-generator.html) you can use to generate the YAML needed for GitHub issue templates. This will allow you to customize the input fields and collect whatever information you need for each type of submission.

A deep link to a specific issue template form will look like this:

`https://github.com/username/Repo-Name/issues/new?template=song-requests.yml`

You can use these to link to the forms directly from your README.md.

Here is what that would look like:
```
Taking [song requests](https://github.com/username/Repo-Name/issues/new?template=song-requests.yml) between 8 PM PST and 10 PM PST every weekday evening.

```

> **PRO TIP:** you can automatically link to an existing issue in a Github comment anywhere else in your repo by simply including the number sign and the corresponding issue number.

```
This is directly related to #25 and will be addressed on the upcoming episode, along with #4 
```

That snippet will automatically link to those issues, assuming they exist.

After you fill out the fields for a GitHub issue form, it will appear in your repo under the Issues tab. Go there to see the new submission, then post a comment. The comments become EMAILS, either between the original sender and the staff, or between staff members discussing the submission.

Here is a quick email template in markdown that you can copy and paste into a comment on GitHub to format it in a way that simulates an email:

## BASIC EMAIL IN MARKDOWN

````markdown
|              |                                                |
| ------------ | ---------------------------------------------- |
| **From:**    | Name, Title/Role `<sender@organization.com>`    |
| **To:**      | Name, Title/Role `<recipient@organization.com>` |
| **Subject:** | Re: [ISSUE TITLE]                              |

```text
Email body text goes here.
```

—Name  
**Title/Role**  
*Name of Organization*


````

The values for From and To would change depending on the sender and recipient, and the subject line would remain the title of the issue being discussed, with Fwd: or Re: at the beginning to indicate forward or reply.

This process of back and forth replies in one place creates a **[THREAD](../Content-Types/THREAD.md)**.

## EMAIL WITH SIGNATURE

````markdown
|||
|---|---|
| **From:** | First Last, Title/Position `<name@show.com>` |
| **To:** | First Last, Title/Position `<redacted@redacted.com>` |
| **Subject:** | Re: Subject Line  |

```text
Body of email goes here.
```

-First Last
**Title/Position**
*Name of Show*
````

## EMAIL WITH FILE ATTACHMENT

````markdown
|              |             |
| ------------ | ----------- |
| **From:**    | First Last, Title `<title@website.com>`    |
| **To:**      | First Last, Title `<name@website.com>`      |
| **Subject:** | Fwd: Subject Line |

```text
Email  body text goes here.
```

- First Last
**Title/Role**
*Show Name*

| ATTACHMENTS | SIZE |
|---|---:|
| 🖼️ **[filename](https://link.com)** | 3 kb |
````

## GITHUB PROJECTS

Use filtered GitHub Project views to simulate **[ACCOUNT](../Content-Types/ACCOUNT.md)** inboxes.

![github-projects](../IMAGES/github-projects.png)

As you can see in the screenshot, the submissions are listed and the label identifies which type of submission each one is. The status column lists which Account the email is currently sitting in.

For example, if all submissions get routed to one address ([producer@show.com](mailto:producer@show.com)) then the status column for all of them would list Producer.

If the Producer forwards the submission to the show's Host, write a new comment representing the forwarding email, then manually change the status from Producer to Host. This moves the thread into the Host’s filtered inbox view.

You can see these different views as tabs in the screenshot below, which shows Paul's Inbox.

The producer for my podcast is named Paul, and the host of the podcast is named Derek.

![account-inboxes](../IMAGES/account-inboxes.png)

You can also see the workflow here, showing that any new issue (submission) gets automatically sent to Paul's Inbox.

![project-default-workflows](../IMAGES/project-default-workflows.png)

You can include the text for each episode or other type of publication as a markdown (.md) file, but if you want more control and advanced formatting for the episodes hosted on the GitHub Pages website, then you should create an HTML file for each one also.

Create a folder in your GitHub repo called /episodes.

Save the Markdown version as `episodes/episode-1.md`, with an optional HTML version alongside it.

`episode-1.html` would be the version that people can view from the GitHub Pages site.

To include a listing of all the available or published episodes for your show, you can add a markdown table to your README.md file and list the title and number of each one.

Here is a markdown snippet template you can use for that:

## EPISODE ARCHIVE MARKDOWN

```
<!-- EPISODES_TABLE_START -->

| Episode No. | Title                                                                         |
|------------:|-------------------------------------------------------------------------------|
|           1 | [EPISODE ONE](./episodes/episode-1.md)                     |
|           2 | [EPISODE TWO](./episodes/episode-2.md)                  |
|           3 | [EPISODE THREE](./episodes/episode-3.md)                                     |
|           4 | [EPISODE FOUR](./episodes/episode-4.md)                  |
|           5 | [EPISODE FIVE](./episodes/episode-5.md)                              |
|           6 | [EPISODE SIX](./episodes/episode-6.md)                        |
|           7 | [EPISODE SEVEN](./episodes/episode-7.md)          |
|           8 | [EPISODE EIGHT](./episodes/episode-8.md)   |
|           9 | [EPISODE NINE](./episodes/episode-9.md)                              |
|          10 | [EPISODE TEN](./episodes/episode-10.md) |

<!-- EPISODES_TABLE_END -->

```

Obviously fill it in with the actual titles of your episodes and be sure you're adding the episode .md files to an /episodes folder if you want to use the URL convention included, or simply change and update it to your folder structure.

