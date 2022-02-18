# Welcome to Brev! 🤙
Brev is a cloud computer for local development. Use your local tools with a dedicated cloud computer.

##  Getting Started

1.  **Download the CLI**

    ```
    brew install brevdev/homebrew-brev/brev
    ```


2. **Create an account:** 
    
    ```
    brev login
    ```
    This will create an account if you don't have one and prompt you to create an SSH key 


3. **Create your first workspace**
    ```zsh
    brev start <git_url>
    ```
    *Note, running this the first time might take a few minutes. Startup times will increase with the next major release (Eta March 2022).*


4. **Connect your computer to your cluster**

    Brev creates a connection from your local computer to your cluster by running the background daemon

    ```
    brev run-tasks -d
    ```

5. **Start Coding! 🤙**
    You are now ready to ssh into your workspace! You can find it by running

    ```
    brev ls
    ```

    Open VS Code to your workspace with 
    
    ```
    brev open workspace_name
    ```

    Follow the guide [here](/howto/connect-via-jetbrains/) for Jetbrains products

    
6. **Make your environment reproducible**

    Create your .brev/setup.sh script to make your environment reproducible. 

    If your repo contains a `.brev/setup.sh` script, Brev will automatically run it when creating the workspace.

    
    We automatically create the setup script for you. Populate it and commit it to your repo. Read more [here](/reference/dot-brev-setup-script/)

7. (Optional) Configure brev to [autostart ssh proxy daemon](/howto/configure-ssh-proxy-daemon-at-boot/) so you don't have to run [run-tasks](/reference/brev-cli#run-tasks) on boot.

If you run into any issues, run `brev refresh`.

Not sure what your workspace is called? Try `brev ls`.

Wrong organization? Try `brev ls orgs` and then `brev set <org_name>`.

View the full [CLI docs here](/reference/brev-cli), and reach out to us in the [Discord](https://discord.gg/NVDyv7TUgJ) for help! We're here for anything you need. Build something great 🤙
