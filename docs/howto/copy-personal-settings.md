# How To
## Copy Personal Settings
You probably have specific settings you wanna bring to every workspace, but only on your workspaces.

Brev.dev supports each developer having their own setup script. The repo has a `.brev/setup.sh` file that gets run on every single workspace, but Brev.dev also runs each developer's personal `.brev/setup.sh` if it exists.


## Create a Personal Settings Repo

From [the console](https://console.brev.dev){:target="_blank"}, go to your profile by clicking "Account" on the top-right.
![Screenshot](media/personal-settings-2.png)
<!-- ![Screenshot](media/personal-settings.png) -->

You'll see a section called **Personal Settings**. This has a git repo that Brev.dev clones into every workspace and runs the `.brev/setup.sh` it contains.

To setup your personal settings:

1. [Click here to fork the personal settings repository](https://github.com/brevdev/user-dotbrev/fork) (you can make your forked repo private if you like)

2. Copy the new url, and paste it in the input field under **Personal Settings** and click the save button.

You're done!

Now every workspace will clone this repo and run your personal settings.


## Make it yours!

Clone your forked repo-- or from any workspace, cd into `/workspace/user-dotbrev`. Commit and push any changes and your next Brev.dev workspace will automatically clone the latest.