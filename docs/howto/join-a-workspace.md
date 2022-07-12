# How to Join a Workspace 

to join a workspace in your orginization, you can run 
`brev start <workspace name>` where `<workspace name>` is the name of a 
workspace that another member of that org has started. 

to list workspaces in your org, run 
```
brev ls --all
```

which has an output similar to

```
You have 1 workspaces in Org brev.dev
 NAME                             STATUS    URL                                                                       ID        
 brev-cli                         RUNNING   brev-cli-p09m-brevdev.wgt-us-west-2-test.brev.
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

the workspaces that I can join are at the bottom of this output 

```
6 other projects in Org brev.dev
 NAME                        MEMBERS 
 brev-landing-page                 2 
 todo-app                          1 
 vagrant-guide                     1 
 mern-template                     1 
 solidity-nextjs-starter           1 
 akka-http-quickstart-scala        1 
 ```

 to join the workspace `brev-landing-page` run

 ```
 $ brev start brev-landing-page
 ```

 which has an output similar to 

 ```
Name flag omitted, using auto generated name: brev-landing-page
Workspace is starting. This can take up to 2 minutes the first time.

name brev-landing-page
template v7nd45zsc Admin
resource class 2x8
workspace group brev-test-brevtenant-cluster
You can safely ctrl+c to exit
⣟  workspace is deploying Connect to the workspace:
        brev open brev-landing-page     # brev open <NAME> -> open workspace in preferred editor
        brev shell brev-landing-page    # brev shell <NAME> -> ssh into workspace (shortcut)
        ssh brev-landing-page-i9rg      # ssh <SSH-NAME> -> ssh directly to workspace
```