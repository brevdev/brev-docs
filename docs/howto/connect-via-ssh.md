# Connect to a Brev workspace using SSH

- Make sure you have the [Brev CLI installed](/)
- Make sure you have [configured brev daemons](/howto/configure-brev-daemons)

to find the lists of available workspaces to ssh into, run 
```
$ brev ls

You have 12 workspaces in Org brev.dev
NAME                                     STATUS             ID            URL
workspace-group                          RUNNING            1le7nnxei     workspacegroup-nxei-brevdev.brev.sh

Connect to your machine with one of the following:
	ssh workspacegroup-nxei

```

and then ssh into the workspace that you want to connect to with

```
ssh workspacegroup-nxei
```

