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

***That's it! 🤙***
