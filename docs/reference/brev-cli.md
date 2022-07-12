# Brev CLI Reference
The Brev CLI is the preferred interface for Brev, allowing you to use cloud computers with your local development tools. Our goal is to be as invisible as possible.

Every command has a `--help` flag if you need to see options.

Brev CLI commands are broken up into 4 categories
Workspace commands, Context commands, SSH commands, and Housekeeping commands.

### Workspace Commands

#### delete
If you no longer need a machine, and you'd like an action more permanent than [stop](/reference/brev-cli/#stop), you can delete the workspace.

`brev delete workspace_name`

#### reset

###### Description
 This command deletes your machine and gets you a fresh one. Make sure to have a [.brev setup script](/reference/dot-brev-setup-script/) or you'll have to reinstall everythign manually.

**Note: even if not committed, the `.brev/setup.sh` script will persist because everythign in `/home/workspace` will be saved.
👆 This makes it really easy to change your environment without needing to commit the changes to main.**

##### Example
reset a workspace with the name `payments-frontend`

```
$ brev reset payments-frontend
Workspace payments-frontend is resetting.
Note: this can take a few seconds. Run 'brev ls' to check status

```

#### run-tasks
This starts the brev daemon. This should be automatically running in the background. This daemon manages the connection between your local computer and each of your remote machines. If you'd like to manually start brev, simply run `brev run-tasks`. If you'd like to make this a background process, add a `-d` to the end.

```
brev run-tasks -d
```

This will have to be run every time you reboot unless you configure [autostart](/howto/configure-ssh-proxy-daemon-at-boot)


#### start

create start and join a workspace 
#### Synopsis

```

brev start { ARG | -e} {-n | --name} {-c | --class} { -s | --setup-script} 
	{-r | --setup-repo} {-p | --setup-path } { -o | --org}
```

#### Description

brev start can do the following:

- start a stopped workspace
- join a workspace in an organization
- create an empty workspace
- create a workspace from a directory on your computer 
- create a workspace from a git url

##### Start A Stopped Workspace 

If you have a workspace in a stopped state, you can start it by using its id 
or workspace name. If you have a workspace named `frontend` that you either 
created or joined that is in a `STOPPED` state, you can start it again by running

```
$ brev start frontend
```

to get find your workspace name or id, see [finding your workspace](howto/find-your-workspace). 

##### Join a Workspace in an Organization



#### Flags

##### -n --name <name>

specify the name for your workspace instead of brev-cli generating one for you.

for example, to override the name of a workspace when creating a workspace from 
a git repo you could do it with then `-n` flag. This example creates a repo with 
the name `cli` from the git repo `https://github.com/brevdev/brev-cli`.

```
$ brev start https://github.com/brevdev/brev-cli -n cli
```


#### Examples
##### Create an empty workspace

```
$ brev start -e -n foo
```

which has an output similar too:

```
name foo
template 4nbb4lg2s ubuntu
resource class 2x8
workspace group brev-test-brevtenant-cluster
workspace is starting. this can take up to 2 minutes the first time.

you can safely ctrl+c to exit
⣽  workspace is deploying
your workspace is ready!

connect to the workspace:
	brev open foo	# brev open <name> -> open workspace in preferred editor
	brev shell foo	# brev shell <name> -> ssh into workspace (shortcut)
	ssh foo-8j4u	# ssh <ssh-name> -> ssh directly to workspace

```

or

```
$ brev start --empty --name foo
```

which has an output similar too:

```
name foo
template 4nbb4lg2s ubuntu
resource class 2x8
workspace group brev-test-brevtenant-cluster
workspace is starting. this can take up to 2 minutes the first time.

you can safely ctrl+c to exit
⣽  workspace is deploying
your workspace is ready!

connect to the workspace:
	brev open foo	# brev open <name> -> open workspace in preferred editor
	brev shell foo	# brev shell <name> -> ssh into workspace (shortcut)
	ssh foo-8j4u	# ssh <ssh-name> -> ssh directly to workspace

```

view your workspace with `brev ls`


##### create a workspace, and do not block shell until workspace is created

use the `-d` or `--detached` flag to create a workspace and immediately exit
rather than wait for workspace to be successfully created before exiting.

```
$ brev start -d -e -n bar
```

which has an output similar too:

```
name bar
template 4nbb4lg2s ubuntu
resource class 2x8
workspace group brev-test-brevtenant-cluster
Workspace is starting. This can take up to 2 minutes the first time.
```

##### Create a workspace from a file path

if in your current directory has a directory in it called `merge-json`, you can
create a workspace using the contents of that directory using
`brev start merge-json`

```
$ ls
merge-json
```

```
$ brev start merge-json

```

which has an output similar too:

```
Workspace is starting. This can take up to 2 minutes the first time.

name merge-json
template 4nbb4lg2s ubuntu
resource class 2x8
workspace group brev-test-brevtenant-cluster
You can safely ctrl+c to exit
⡿  workspace is deploying
Your workspace is ready!

Connect to the workspace:
	brev open merge-json	# brev open <NAME> -> open workspace in preferred editor
	brev shell merge-json	# brev shell <NAME> -> ssh into workspace (shortcut)
	ssh merge-json-wd6q	# ssh <SSH-NAME> -> ssh directly to workspace
```

##### Create a workspace from a git repository


```
$ brev start https://github.com/brevdev/react-starter-app
```

which has an output similar too:

```
Workspace is starting. This can take up to 2 minutes the first time.

name react-starter-app
template 4nbb4lg2s ubuntu
resource class 2x8
workspace group brev-test-brevtenant-cluster
You can safely ctrl+c to exit
⣾  workspace is deploying
Your workspace is ready!

Connect to the workspace:
	brev open react-starter-app	# brev open <NAME> -> open workspace in preferred editor
	brev shell react-starter-app	# brev shell <NAME> -> ssh into workspace (shortcut)
	ssh react-starter-app-8v8p	# ssh <SSH-NAME> -> ssh directly to workspace

```

##### Join a workspace in your orginization

view your orgs workspaces with `brev ls --all`. Workspaces in your org that you
have not joined appear at the bottom of the output.

```
$ brev ls --all
```

which has an output similar too:

```
You have 1 workspace in Org brev.dev
 NAME                             STATUS    URL                                                                       ID
 brev-cli                         RUNNING   brev-cli-p09m-brevdev.wgt-us-west-2-test.brev.dev                         x1yxqp09m

Connect to running workspace:
	brev open brev-cli	# brev open <NAME> -> open workspace in preferred editor
	brev shell brev-cli	# brev shell <NAME> -> ssh into workspace (shortcut)
	ssh brev-cli-p09m	# ssh <SSH-NAME> -> ssh directly to workspace

7 other projects in Org brev.dev
 NAME                        MEMBERS
 new-docs                          1
 brev-landing-page                 2
 todo-app                          1
 vagrant-guide                     1
 mern-template                     1
 solidity-nextjs-starter           1
 akka-http-quickstart-scala        1

Join a project:
	brev start new-docs

```

join the project new-docs

```
$ brev start new-docs
```

which has an output similar too:

```
Name flag omitted, using auto generated name: new-docs
Workspace is starting. This can take up to 2 minutes the first time.

name new-docs
template 4nbb4lg2s ubuntu
resource class 2x8
workspace group brev-test-brevtenant-cluster
You can safely ctrl+c to exit
⣟  workspace is deploying Connect to the workspace:
	brev open new-docs	# brev open <NAME> -> open workspace in preferred editor
	brev shell new-docs	# brev shell <NAME> -> ssh into workspace (shortcut)
	ssh new-docs-pek9	# ssh <SSH-NAME> -> ssh directly to workspace
```

##### Start a stopped workspace

If you have already joined a workspace and have stopped it with `brev stop`,
you can start it again with `brev start`

view your current workspaces with `brev ls`

```
$ brev ls
```

which has an output similar too:

```
You have 1 workspace in Org brev.dev
 NAME                             STATUS     URL                                                                       ID
 linear-client                    STOPPED    linear-client-yw1a-brevdev.wgt-us-west-2-test.brev.dev                    gov5jyw1a

Connect to running workspace:
	brev open linear-client	# brev open <NAME> -> open workspace in preferred editor
	brev shell linear-client	# brev shell <NAME> -> ssh into workspace (shortcut)
	ssh linear-client-yw1a	# ssh <SSH-NAME> -> ssh directly to workspace

```
join the workspace
```
$ brev start linear-client
```

which has an output similar too:

```
Workspace linear-client is starting.
Note: this can take about a minute. Run 'brev ls' to check status

You can safely ctrl+c to exit
```


**Note: if you want to make multiple workspaces with the same git repo, use the --name flag with brev start**
You can have multiple workspaces with the same git repo, however, each workspace must have a unique name.

#### stop
If you don't plan on using your Brev workspace, you can temporarily pause it by running
```zsh
brev stop workspace_name
```
Everything in `/home/workspace` will be saved when it boots up again.

stop multiple workspaces
```
$ brev stop brev-deploy naive-pubsub bar euler54 merge-json
Workspace brev-deploy is stopping.
Note: this can take a few seconds. Run 'brev ls' to check status
Workspace naive-pubsub is stopping.
Note: this can take a few seconds. Run 'brev ls' to check status
Workspace bar is stopping.
Note: this can take a few seconds. Run 'brev ls' to check status
Workspace euler54 is stopping.
Note: this can take a few seconds. Run 'brev ls' to check status
Workspace merge-json is stopping.
Note: this can take a few seconds. Run 'brev ls' to check status
```

### Context Commands
Brev commands run within the context of an organization, this way it's really clear if something is running under your personal account or under your organization's. Most commands support an `--active-org` flag for scripting purposes.

#### ls
Print a tabular view of your workspaces or orgs

```zsh
# print orgs
brev ls orgs

# print workspaces within active organization
brev ls

# print workspaces within any organization
brev ls --org org_name
```

#### set
Set the organization context for your commands.
```zsh
brev set <org name>
```

### SSH Commands
Brev aims to be as invisible as possible, letting developers code locally with the benefits of cloud compute. The commands in this section will evolve to happen in the background as much as makes sense.

#### port-forward
You can always access the localhost URL of your workspace via the [public url](/howto/find-my-localhost/), or you can port-forward your remote localhost to a local one.

Run
```zsh
brev port-forward workspace_name --port localport:remoteport
```

For example, to run the brev docs on port 3000:
```zsh
brev port-forward brev-docs --port 3000:3000
```

This command runs interactive if the ports flag is left off.

![Screenshot](media/localpublic.png)

### Housekeeping Commands

#### jetbrains
Jetbrains, unfortunately, doesn't use the standard SSH file, and instead uses a custom XML file. To establish a connection between your local computer and all of the workspaces in your organization, run:

```zsh
brev jetbrains
```

This command runs a helper proxy for jetbrains products that allows your jetbrains IDEs ssh access. It does *not* update if new workspaces are created or deleted, so please stop the process and re-run it to update it.

Note: this will hold your shell. Keep this process running to keep the connection live. If there's a timeout for whatever reason, please ctrl+c and re-run `brev jetbrains`.

#### login
Authenticate yourself with
```zsh
brev login
```
This will create an account if you don't already have one.

#### logout
Remove your keys and logout
```zsh
brev logout
```

#### profile
If you have personal settings, such as aliases or shortcuts in your `~/.zshrc` or `~/.bash_profile`, you can sync them with Brev.dev to make sure every workspace you create has them.

Create a git repo with setup script at `~.brev/setup.sh` or fork our example [here](https://github.com/brevdev/user-dotbrev). Once your setup is copied over, add it to your profile with

```zsh
brev profile --set-personal-config _git_repo_url_
```

#### refresh
As a troubleshooting measure, you can force the cache to refresh if you suspect they're stale.
```zsh
brev refresh
```

#### secret
Use the encrypted secrets manager to load secret files and environment variables into your workspace, or set them for the entire org.

Run the command in interactive mode by ommitting the flags
```zsh
brev secret
```

A secret file or environment variable needs a name and a value, the scope to be set (org or private), a type (variable or file). If the secret is a file, you'll also need to supply the path

Ex: personal environment variable
```zsh
  brev secret --name SERVER_URL --value https://brev.sh --type variable --scope personal
```

Ex: personal AWS credentials file
```zsh
  brev secret --name AWS_KEY --value ... --type file --file-path --scope personal
```

#### ssh-key
Get your ssh keys to add to your git provider.
```zsh
brev ssh-key
```
Quick links to add it to [Github](https://github.com/settings/keys) or [Gitlab](https://gitlab.com/-/profile/keys)
