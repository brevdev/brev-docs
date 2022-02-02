# Welcome to Brev 🤙
Brev is a cloud computer for local development. Use your local tools with a dedicated cloud computer.

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

2. Run `brev login`. If you don't already have an account, this will create one and prompt you to create an SSH key.

    **Your account must be verified to create a workspace. You can verify by putting a credit card on file (we'll never charge you without your permission) or just message us in the [Discord](https://discord.gg/NVDyv7TUgJ).**

3. Use the `start` command to create your first workspace. *Note, running this the first time might take a few minutes. We're aware of this issue and are working on it.*

    ```zsh
    brev start <git_url>
    ```

4. connect your local computer to your cluster by running the background daemon

    ```
    brev run-tasks -d
    ```

5. you are now ready to ssh into your instance! you can find it by running

    ```
    brev ls
    ```

6. (Optional) Configure brev to [autostart ssh proxy daemon](/howto/configure-ssh-proxy-daemon-at-boot/) so you don't have to run [run-tasks](/reference/brev-cli#run-tasks) on boot.

If you run into any issues, run `brev refresh`.

Not sure what your workspace is called? Try `brev ls`.

Wrong organization? Try `brev ls orgs` and then `brev set <org_name>`.

View the full [CLI docs here](/reference/brev-cli), and reach out to us in the [Discord](https://discord.gg/NVDyv7TUgJ) for help! We're here for anything you need. Build something great 🤙
