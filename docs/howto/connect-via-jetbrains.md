# Connect to a Brev workspace using JetBrains

Make sure you have the [Brev CLI installed](/)

---

_This includes Webstorm, GoLand, IntelliJ IDEA, PyCharm etc._

You will need to open JetBrains Gateway instead of your locally installed JetBrains IDE. It will install the language process server and other heavyweight processes on the remote machine, while exposing the client of the IDE to you.

We guide you through this process the first time you download the CLI, but a link to manually download the software is here: [jetbrains.com/remote-development/gateway](https://www.jetbrains.com/remote-development/gateway/)

## Important Caveat 

when you make the inital ssh connection to your brev workspace, your local computer does not recognise the remote host's public key  (since this is the first time it has connected to it), and then prompts for the user to continue connecting and associate this public key with that host with the message:

```
The authenticity of host '203.0.113.1 (203.0.113.1)' can't be established.
ECDSA key fingerprint is fd:fd:d4:f9:77:fe:73:84:e1:55:00:ad:d6:6d:22:fe.
Are you sure you want to continue connecting (yes/no)? yes
```

unfortunately at this time, this message will break Gateway when trying to connect to a workspace. 

You can work around this issue by making sure that you have ssh'ed into the workspace once before. 

For example, if i create a workspace called `foo-frontend` and I want to connect to it via Jetbrains Gateway, I need to first ssh into the workspace 
```
ssh foo-frontend
```

accept the host prompt

```
The authenticity of host '203.0.113.1 (203.0.113.1)' can't be established.
ECDSA key fingerprint is fd:fd:d4:f9:77:fe:73:84:e1:55:00:ad:d6:6d:22:fe.
Are you sure you want to continue connecting (yes/no)? yes
```

and then connecting the workspace via Jetbrains Gateway. We are looking forward to configuring your workspace to be recognised by your local machine in upcoming releases of brev. 
 

## Connect to a Workspace  

1. Make sure you have [configured brev daemons](/howto/configure-brev-daemons).

2. Open JetBrains Gateway and select "Connect Via SSH".
![Screenshot](media/jetbrains1.png)

3. Your Brev machines should already be listed for you! Select the correct machine and click "Check Connection and Continue". If you do not see your brev machine, [skip to the end](#do-it-manually) of this to manually add ssh connection details 👇
![Screenshot](media/jetbrains2.png)

4. Select the IDE you'd like to use. Enter the project directory. This will always be `/home/brev/workspace/<GIT_REPO_OR_PROJECT_NAME>`. If you don't know the GIT_REPO_OR_PROJECT_NAME, simply click on the folder icon to find the correct folder. Click Download and Start IDE! That's it!
![Screenshot](media/jetbrains3.png)

---

## Do It Manually

To manually add SSH connection details:

1. Select `<New Connection>` from the Connection dropdown
![Screenshot](media/jetbrains5.png)

2. Enter the following information:
	* **Username:** brev
	* **Host:** localhost
	* **Private Key:** `<ROOT>/.brev/brev.pem`. `ROOT` is ~, in Mac this would be `/Users/<USERNAME>`. You must enter the absolute path, relative paths will not work.
	* **Save Passphrase:** Unchecked
	* **Port:** Select the port of the brev project displayed in your terminal after entering brev up. See example below:
![Screenshot](media/jetbrains6.png)

3. Go back to step 3) and continue from there 🙂
