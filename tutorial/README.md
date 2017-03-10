Tutorial
========

Here is a step-by-step tutorial on how to use this command-line
tool to integration with [HipChat][hc].  This tutorial only
describes `v2` access.

## Obtaining an Access Token

In order to talk to the hipchat servers, you will require an access
token.  This is easily obtained from your profile.

Log in to your site's home page, http://_site_.hipchat.com

![HipChat Home Page](image/01-frontpage.png)

From the home page, click on the Edit Profile button.
That should bring up your profile page:

![Profile Page](image/02-editing-profile.png)

There, on the left menu is a panel for **API access**.  Click
that to bring up the API access management page:

![API Access Page](image/04-create-key.png)

At the bottom of that page is a **Create new token** section;
select the scopes you want (for normal posting of messages
to a room, all you need is the _Send Notification_ scope).
Give the token a label so you can remember later why you created
it, and click **Create**.
That should update the page to include the new token:

![New Token Display](image/05-created-key.png)

The Personal token is the one you want.  Save it off for later use.

## Obtaining a Room API ID

[hc]: http://www.hipchat.com
