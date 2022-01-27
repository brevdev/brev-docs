# Welcome to Brev 🤙
Brev is a cloud computer for local development. Use your local tools with a dedicated cloud computer. 

##  Getting Started

1.  Start by downloading the CLI:
    ```zsh
    sudo sh -c "`curl -sf -L https://raw.githubusercontent.com/brevdev/brev-cli/main/bin/install-latest.sh`" && export PATH=/opt/brev/bin:$PATH && brev run-tasks -d && brev login
    ```
    **Apple Silicon (M1) Mac?** You'll need to run rosetta first:
    ```zsh
    # for M1 macs only
    softwareupdate --install-rosetta
    ```

2.  Add the `brev` command to your path:

    **zsh**
    ```zsh
    # zsh
    export PATH=/opt/brev/bin:$PATH
    echo PATH=/opt/brev/bin:$PATH >> ~/.zshrc
    ```
    **Bash**
    ```zsh
    # bash
    export PATH=/opt/brev/bin:$PATH
    echo PATH=/opt/brev/bin:$PATH >> ~/.bashrc
    ```

4. Run `brev login`. If you don't already have an account, this will create one and prompt you to create an SSH key.

    **Your account must be verified to create a workspace. You can verify by putting a credit card on file (we'll never charge you without your permission) or just message us in the [Discord](https://discord.gg/NVDyv7TUgJ).**

5. Use the `start` command to create your first workspace. *Note, running this the first time might take a few minutes. We're aware of this issue and are working on it.*
```zsh
brev start <git_url>
```

***That's it 🤙***

If you run into any issues, run `brev refresh`.

Not sure what your workspace is called? Try `brev ls`.

Wrong organization? Try `brev ls orgs` and then `brev set <org_name>`.

View the full [CLI docs here](/reference/brev-cli), and reach out to us in the [Discord](https://discord.gg/NVDyv7TUgJ) for help! We're here for anything you need. Build something great 🤙