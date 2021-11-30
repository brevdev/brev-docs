# Connect to a Brev workspace using Emacs

Make sure you have the [Brev CLI installed](/)

In emacs execute `M-x dired RET` and enter the directory

```
/ssh:<workspace-name>:/home/brev/workspace/vue-coffee
```


---

You'll need to have a running workspace. If you don't have one yet:

Deploy a new workspace with [brev start](/reference/brev-cli/#start)
```shell
$ brev start https://github.com/just-fine/vue-coffee
Workspace is starting. This can take up to 2 minutes the first time.

⣻  workspace is deploying
Your workspace is ready!

SSH into your machine:
	ssh just-fine/vue-coffee

```

Wait until your workspace is done deploying and then, in a seperate terminal, run [brev up](/reference/brev-cli/#up): 

```shell
$ brev up
Setting up client...
Resolving workspaces...
Running up...
Editing ssh config, backed up at path /home/f/.brev/config.bak.ee755c95-c3c4-4f35-9305-f5c88cf86207

ssh just-fine/vue-coffee

Forwarding from 127.0.0.1:2229 -> 22

```
