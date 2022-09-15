# How To Find My Dev Environment Name or ID


## Find your Dev Environment ID or Name

You can find this information by running:

```
$ brev ls 
```
which has an output similar to

```
You have 1 Dev Environment in Org brev.dev
 NAME                             STATUS    URL                                                                       ID       
 brev-cli                         RUNNING   brev-cli-p09m-brevdev.wgt-us-west-2-test.brev.dev                         x1yxqp09m 
 
Connect to running dev environment:
        brev open brev-cli      # brev open <NAME> -> open environment in preferred editor
        brev shell brev-cli     # brev shell <NAME> -> ssh into environment (shortcut)
```

## Find dev environments in your org to clone

You can go to the [Team Templates tab in the console] to see dev environments you or your team have created. Click clone to make a copy, Brev won't copy their personal settings and will install your personal settings.

<!-- ## See Also 

- [How To Join a Workspace](howto/join-a-workspace) -->