# Brev Debugging

This page has common hurdles or known issues that we're addressing.


##  Reset Brev
If you're noticing some workspaces to be missing, use the Brev refresh command to try forcing a refresh to the ssh config and ensuring the daemon is started:

```zsh
brev refresh
```
##  500 error when running `brev start`
If you run `brev start` and see the following 500 error:

```zsh
➜  ~ brev start https://github.com/brevdev/hello-react
Name flag omitted, using auto generated name: brevdev/hello-react
Workspace is starting. This can take up to 2 minutes the first time.

[error] /home/runner/work/brev-cli/brev-cli/pkg/cmd/start/start.go:260 
	: https://ade5dtvtaa.execute-api.us-east-1.amazonaws.com/api/organizations/ejmrvoj8m/workspaces?utm_source=cli 500 Internal Server Error
```
It is likely that you just deleted the workspace and it is still deleting. Please wait 5 seconds and try again.


## Workspace version issue
If you've used Brev with older version of the CLI, it's likely that your workspaces need to be upgraded. You might see an error like this:

```zsh
workspace of version v1.6.8 is not supported with this cli version\n upgrade your workspace or downgrade your cli"
```

There isn't a command to upgrade the workspaces yet, so in the interim, please delete the workspace and create it again.

```zsh
brev delete brev-cli
```

```zsh
# if someone else in your org has the workspace
brev start https://github.com/brevdev/brev-cli 
```

or if someone else in your org has the same workspace, you can `brev start` by name to create your own workspace. Run `brev ls --all` to see workspaces already in your org.

```zsh
# if someone else in your org has the workspace
brev start brev-cli 
```

##  Global npm install issues
If you try npm installing something globally, it might not work without sudo.

Rerun the command with sudo, ex `sudo npm install http-server -g`. Reach out to support if you're still having issues: https://discord.gg/NVDyv7TUgJ

##  See all the startup logs
Sometimes weird issues happen when configuring the machine, for example, the project folder is empty because ssh keys weren't configured and the repo couldn't be cloned. 

You can view the full startup logs by running `sudo cat /var/log/brev-workspace.log` inside your workspace.

##  Run Brev without internet
Do you want to run Brev.dev locally without needing internet? We're launching the V2 in late June and would love for you to try it! Hop in the discord and let us know you're waiting for it! https://discord.gg/NVDyv7TUgJ
