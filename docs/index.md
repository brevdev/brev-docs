# Welcome to Brev 🤙
Brev is a cloud computer for local development. Use your local tools with a dedicated cloud computer. 

##  Getting Started

1.  Start by downloading the CLI:
```zsh
sudo sh -c "`curl -sf -L https://raw.githubusercontent.com/brevdev/brev-cli/main/bin/install-latest.sh`"
```

2. Run `brev login`. If you don't already have an account, this will create one and prompt you to create an SSH key.

**Your account must be verified to create a workspace. You can verify by putting a credit card on file (we'll never charge you without your permission) or just message us in the discord.**

3. Use the `start` command to create your first workspace. *Note, running this the first time might take a few minutes. We're aware of this issue and are working on it.*
```zsh
brev start <git_url>
```
4. Once the workspace is ready, run Brev up to connect your local machine to your remote machines via SSH
```zsh
brev up
```
*Note: keep this shell running to keep the connections live. You might need to kill and restart the process if your computer shuts off (ctrl+c then `brev up`). We might make this a background process in the future.*

5. To access a port locally, use the `port-forward` command
```zsh
brev port-forward <workspace_name> --port localport:remoteport
```
So if your workspace name is "brevdocs" and it's running on port 3000, run the following:
```zsh
brev port-forward brevdocs --port 3000:3000
```

Not sure what your workspace is called? Try `brev ls` to print orgs in your active org. You can view orgs with `brev ls orgs` and change active orgs with `brev set <org_name>`.

View the full [CLI docs here](/reference/brev-cli), and reach out to us in the [Discord](https://discord.gg/NVDyv7TUgJ) for help! We're here for anything you need. Build something great 🤙