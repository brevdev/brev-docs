# How To Find My Workspace Name or ID

This depends on if you have joined a workspace or not. 

## Find Workspace ID or Name of workspace that you have joined    

There are many times when using brev it useful to know a workspaces name or id.
You can find this information by running:

```
$ brev ls 
```
which has an output similar to

```
You have 1 workspaces in Org brev.dev
 NAME                             STATUS    URL                                                                       ID       
 brev-cli                         RUNNING   brev-cli-p09m-brevdev.wgt-us-west-2-test.brev.dev                         x1yxqp09m 
 
Connect to running workspace:
        brev open brev-cli      # brev open <NAME> -> open workspace in preferred editor
        brev shell brev-cli     # brev shell <NAME> -> ssh into workspace (shortcut)
        ssh brev-cli-p09m       # ssh <SSH-NAME> -> ssh directly to workspace
Or ssh:
        ssh brev-cli-p09m
```

## Find Workspace name of workspace that you have not joined 

List all workspaces in your current org 

```
$ brev ls --all
```

which should have an output similar to 

```
➜  brev-cli git:(main) ✗ ./brev ls --all
You have 1 workspaces in Org brev.dev
 NAME                             STATUS    URL                                                                       ID        
 brev-cli                         RUNNING   brev-cli-p09m-brevdev.wgt-us-west-2-test.brev.dev                         x1yxqp09m 


Connect to running workspace:
        brev open brev-cli      # brev open <NAME> -> open workspace in preferred editor
        brev shell brev-cli     # brev shell <NAME> -> ssh into workspace (shortcut)
        ssh brev-cli-p09m       # ssh <SSH-NAME> -> ssh directly to workspace
Or ssh:
        ssh brev-cli-p09m
        ssh brev-docs-xp43

6 other projects in Org brev.dev
 NAME                        MEMBERS 
 brev-landing-page                 2 
 todo-app                          1 
 vagrant-guide                     1 
 mern-template                     1 
 solidity-nextjs-starter           1 
 akka-http-quickstart-scala        1 
 ```

at the bottom of this output you can see the other workspaces in this org that 
you can join. 

## See Also 

- [How To Join a Workspace](howto/join-a-workspace)