# Brev Debugging

This page has common hurdles or known issues that we're addressing.


##  Reset Brev
If you're noticing some workspaces to be missing, use the Brev refresh command to try forcing a refresh to the ssh config and ensuring the daemon is started:

```zsh
brev refresh
```

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
