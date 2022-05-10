# Brev CLI

The Brev CLI is the preferred interface for Brev, allowing you to use cloud computers with your local development tools. Our goal is to be as invisible as possible.

Every command has a `--help` flag if you need to see options.

##  Getting Started

1.  Start by downloading the CLI:
if brew is not already installed on your computer install it with
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
then add Brev's tap and install `brev` with
```
brew install brevdev/homebrew-brev/brev
```


3. Run `brev login`. If you don't already have an account, this will create one and prompt you to create an SSH key.
  **Your account must be verified to create a workspace. You can verify by putting a credit card on file (we'll never charge you without your permission) or just message us in the [Discord](https://discord.gg/NVDyv7TUgJ).**


3. Use the `start` command to create your first workspace. *Note, running this the first time might take a few minutes. We're aware of this issue and are working on it.*
```zsh
brev start <git_url>
```

4. Configure brev to [autostart ssh proxy daemon](/howto/configure-ssh-proxy-daemon-at-boot/)
If you run into any issues, run `brev refresh`.

Not sure what your workspace is called? Try `brev ls`.

Wrong organization? Try `brev ls orgs` and then `brev set <org_name>`.

View the full CLI docs below, and reach out to us in the [Discord](https://discord.gg/NVDyv7TUgJ) for help! We're here for anything you need. Build something great 🤙

## Brev CLI Reference

Brev CLI commands are broken up into 4 categories
Workspace commands, Context commands, SSH commands, and Housekeeping commands.

### Workspace Commands

#### delete
If you no longer need a machine, and you'd like an action more permanent than [stop](/reference/brev-cli/#stop), you can delete the workspace.

`brev delete workspace_name`

#### reset
If you're experiencing any machine problems, including self-inflicted ones like installing conflicting or incorrect software versions, rather than wasting time debugging, just bite the bullet. This command deletes your machine and gets you a fresh one. Make sure to have a [.brev setup script](/reference/dot-brev-setup-script/) or you'll have to reinstall everythign manually. 

**Note: even if not committed, the `.brev/setup.sh` script will persist because everythign in `/home/workspace` will be saved.
👆 This makes it really easy to change your environment without needing to commit the changes to main. 

#### run-tasks
This starts the brev daemon. This should be automatically running in the background. This daemon manages the connection between your local computer and each of your remote machines. If you'd like to manually start brev, simply run `brev run-tasks`. If you'd like to make this a background process, add a `-d` to the end.

```
brev run-tasks -d
```

This will have to be run every time you reboot unless you configure [autostart](/howto/configure-ssh-proxy-daemon-at-boot)


#### start
Create a new workspace from a git URL or to start a stopped workspace.

Supplying a git url,
```zsh
brev start git_url
```
 will create a new workspace with the git url cloned. Create a [.brev directory](/reference/dot-brev-setup-script/) and anyone can get their own workspace that comes configured for immediate development.

When viewed from the web dashboard, workspaces within an org become projects, allowing your organization's members to get their own cloned workspace with one click.

If you have a Brev workspace in a stopped state, run
```zsh
brev start workspace_name
```
to start it up again. Note, this might take a minute or two.

**Note: if you want to make multiple workspaces with the same git repo, use the --name flag with brev start**
You can have multiple workspaces with the same git repo, however, each workspace must have a unique name.

#### stop
If you don't plan on using your Brev workspace, you can temporarily pause it by running
```zsh
brev stop workspace_name
```
Everything in `/home/workspace` will be saved when it boots up again.

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
