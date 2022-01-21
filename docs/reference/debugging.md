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
If you've used Brev with older version of the CLI, it's likely that your workspaces need to be upgraded. There isn't a command to upgrade the workspaces yet, so in the interim, please delete the workspace and create it again.

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
