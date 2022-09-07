<!--todo split into multiple docs -->

# Brev CLI Reference

The Brev CLI is the preferred interface for Brev, allowing you to use cloud computers with your local development tools. Our goal is to be as invisible as possible.

Every command has a `--help` flag if you need to see options.

Brev CLI commands are broken up into 4 categories:

- Workspace commands
- Context commands
- SSH command
- Housekeeping commands.

## Workspace Commands

### scale

Scale a dev environment up or down to a different instance

#### Synopsis

```
    brev scale [ Workspace Name or ID... ] --gpu [GPU Instance]

#	or

	brev scale [ Workspace Name or ID... ] --cpu [CPU Instance]
```

#### Description

Move your dev environment to a different size machine. All work, settings, etc will be persisted.
View [available instance types here](/reference/gpu#cpu-instance-types).

#### Examples

##### Scale to a GPU instance

```
$ brev scale brev-environments-ui --gpu g5g.xlarge
```

##### Scale to a CPU instance

```
$ brev scale brev-environments-ui --cpu 2x8
```

### delete

Delete a Workspace by name or ID.

#### Synopsis

```
    brev delete [ Workspace Name or ID... ]
```

#### Description

Deleting a workspace will permanently delete a workspace from your account.
This command will delete all content in the workspace and any volumes associated
with the workspace. This command is not reversable and can result in lost work.

#### Examples

##### Delete a workspace

```
$ brev delete payments-frontend
Deleting workspace payments-frontend. This can take a few minutes. Run 'brev ls' to check status
```

##### Delete multiple workspaces

```
$ brev delete bar euler54 naive-pubsub jupyter
Deleting workspace bar. This can take a few minutes. Run 'brev ls' to check status
Deleting workspace euler54. This can take a few minutes. Run 'brev ls' to check status
Deleting workspace naive-pubsub. This can take a few minutes. Run 'brev ls' to check status
Deleting workspace jupyter. This can take a few minutes. Run 'brev ls' to check status

```

### reset

#### Description

This command deletes your machine and gets you a fresh one. Make sure to have a [.brev setup script](/reference/dot-brev-setup-script/) or you'll have to reinstall everythign manually.

**Note: even if not committed, the `.brev/setup.sh` script will persist because everythign in `/home/workspace` will be saved.
👆 This makes it really easy to change your environment without needing to commit the changes to main.**

#### Example

reset a workspace with the name `payments-frontend`

```
$ brev reset payments-frontend
Workspace payments-frontend is resetting.
Note: this can take a few seconds. Run 'brev ls' to check status

```

### start

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

### stop

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

### port-forward

#### Synopsis

```
	brev port-forward WS_NAME  [--port LOCAL_PORT:REMOTE_PORT]
```

#### Description

port forward allows you to forward a port from a brev workspace to a port on
your local machine.

#### Examples

##### Forward a port from a workspace to localhost

port forward port 3333 on a workspace with the name `brev-docs` to port 3000 on your localhost

```zsh
$ brev port-forward brev-docs --port 3000:3333
```

which has an output similar to

```
2022/07/14 11:29:02 creating new ssh config
portforwarding...
localhost:3000 -> brev-docs-xp43:3333
```

##### Interactively port forward a workspace:

To interacticely select which port to forward from a brev workspace to your
localhost, run brev-port-forward with no flag

```
$ brev port-forward brev-docs

Ports flag was omitted, running interactive mode!

What port on your Brev machine would you like to forward? 3333
What port should it be on your local machine? 3000

-p 3000:3333
2022/07/14 11:31:30 creating new ssh config
portforwarding...
localhost:3000 -> brev-docs-xp43:3333
```

#### See Also

## Context Commands

Brev commands run within the context of an organization, this way it's really clear if something is running under your personal account or under your organization's. Most commands support an `--active-org` flag for scripting purposes.

### ls

Print a tabular view of your workspaces or orgs

```zsh
# print orgs
brev ls orgs

# print workspaces within active organization
brev ls

# print workspaces within any organization
brev ls --org org_name
```

### set

Set the organization context for your commands.

```zsh
brev set <org name>
```

## Housekeeping Commands

### jetbrains

Jetbrains, unfortunately, doesn't use the standard SSH file, and instead uses a custom XML file. To establish a connection between your local computer and all of the workspaces in your organization, run:

```zsh
brev jetbrains
```

This command runs a helper proxy for jetbrains products that allows your jetbrains IDEs ssh access. It does _not_ update if new workspaces are created or deleted, so please stop the process and re-run it to update it.

Note: this will hold your shell. Keep this process running to keep the connection live. If there's a timeout for whatever reason, please ctrl+c and re-run `brev jetbrains`.

### login

#### Synopsis

```
	brev login [--token] [--skip-browser]
```

#### Description

This function log's you in to your brev account, and preforms some actions that
brev needs to function with you user account such as set up config files and

<!--todo  explain this a little clearer -->

- creates `~/.brev/` directory if it does not exist
- if you don't have an account on brev, the browser step will create one for you
- on first run asks you onboarding questions
- on first run asks you to configure ssh keys
- creates your first org if one does not exist
- imports your ide config for your workspaces <!-- todo needs elaboration>
- runs `brev run-tasks -d` <!-- todo link to doc page >

#### Flags

#### Examples

```
$ brev login
```

#### See Also

<!-- todo link to logout page -->

### logout

Remove your keys and logout

```zsh
brev logout
```

### profile

If you have personal settings, such as aliases or shortcuts in your `~/.zshrc` or `~/.bash_profile`, you can sync them with Brev.dev to make sure every workspace you create has them.

Create a git repo with setup script at `~.brev/setup.sh` or fork our example [here](https://github.com/brevdev/user-dotbrev). Once your setup is copied over, add it to your profile with

```zsh
brev profile --set-personal-config _git_repo_url_
```

### refresh

As a troubleshooting measure, you can force the cache to refresh if you suspect they're stale.

```zsh
brev refresh
```

### secret

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

### ssh-key

Get your ssh keys to add to your git provider.

```zsh
brev ssh-key
```

Quick links to add it to [Github](https://github.com/settings/keys) or [Gitlab](https://gitlab.com/-/profile/keys)

### run-tasks

#### Synopsis

```
    brev run-tasks -d
```

#### Description

In order for brev to connect to workspaces, there needs to be background daemons
running to manage some things on your local machines environment. Currently, the
one that is being launched by run-tasks is an ssh config file configuration
daemon that periodically udpates a ssh config file with connection information
in order to access you workspaces.

This command has to be run at every boot, see [Configuring SSH Proxy Daemon at Boot](https://docs.brev.dev/howto/configure-ssh-proxy-daemon-at-boot/) to
configure this command to be run at boot.

This command is set to be deprecated in favor of `brev configure`.

#### Examples

to run tasks in the background

```
$ brev run-tasks -d
PID File: /home/f/.brev/task_daemon.pid
Log File: /home/f/.brev/task_daemon.log
```

to run tasks in the foreground

```
$ brev run-tasks
2022/07/11 15:28:44 creating new ssh config
2022/07/11 15:28:48 creating new ssh config

```

#### See Also

- [Configuring SSH Proxy Daemon at Boot](https://docs.brev.dev/howto/configure-ssh-proxy-daemon-at-boot/)
  -TODO brev configure docs
