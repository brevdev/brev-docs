# Connect to a Brev dev environment using Emacs

Make sure you have the [Brev CLI installed](/)

In emacs execute `M-x dired RET` and enter the directory

```
/ssh:<environment-name>:/home/ubuntu/vue-coffee
```


---

You'll need to have a running dev environment. If you don't have one yet:

Create a new dev environment with [brev start](/reference/brev-cli/#start)
```shell
$ brev start https://github.com/just-fine/vue-coffee
dev environment is starting. This can take up to 2 minutes the first time.

⣻  dev environment is deploying
Your dev environment is ready!

```

***That's it! 🤙***
