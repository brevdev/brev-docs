# How To
## Copy Personal Settings
You probably have specific settings you wanna bring to every dev environment, but only on your dev environments.

Brev supports each developer having their own setup script or dotfiles repo. The repo has a bash script that gets run on every single dev environment, but Brev will also run your personal bash script on your environments if it exists.


## Create a Personal Settings Repo

From [the console](https://console.brev.dev){:target="_blank"}, go to your profile by clicking "Account" on the top-right.
![Screenshot](media/personal-settings-2.png)
<!-- ![Screenshot](media/personal-settings.png) -->

You'll see a section called **Personal Settings**. This has a git repo that Brev clones into every dev environment and runs the bash script it contains. By default, it'll be `.brev/setup.sh` but you can set a different path.

To setup your personal settings:

1. [Click here to fork the personal settings repository](https://github.com/brevdev/user-dotbrev/fork) (you can make your forked repo private if you like)

2. Copy the new url, and paste it in the input field under **Personal Settings** and click the save button.

You're done!

Now every dev environment will clone this repo and run your personal settings.


## Make it yours!

Clone your forked repo-- or from any dev environment, cd into `~/user-dotbrev`. Commit and push any changes and your next Brev environment will automatically clone the latest.