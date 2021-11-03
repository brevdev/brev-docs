# Reference

## The .brev directory

Creating a .brev setup script for each Brev project will standardize dependencies, packages and tools across all developers contributing to the same project (ex. Node v14, Yarn v1.22). By default, Brev will create a /.brev/setup.sh script in your workspace. If you commit this to your repo, it will get executed for every new Brev machine. 

The setup scripts run from the project directory, so `/home/brev/<PROJECT_FOLDER_NAME>`

## .brev/setup.sh
This is the main configuration file that runs on your Brev machine, directly after we provision it and before your project is cloned.

The working directory when the file is running is `/home/brev/<PROJECT_FOLDER_NAME>`.

Careful not to place user settings in here (like VSCode extensions or settings) unless you want to impose them for every contributor in the project. Sometimes this is desireable, for example, to standardize linting practices across the team.

A log file with output from the script. It is located at `./.brev/logs/setup.log`. We strongly encourage echo-ing statements into this file when installing new software to know where errors might be located.

## .brev/ports.yaml
You can specify which ports you want publicly accessible. By default, any connection to your project is password protected. Although this is secure, it prevents testing routes, connecting different services (like a backend and frontend), and publicly sharing your project.

Use this file to make your localhost url publicly accessible and share it with others. Be sure to never share your password!

For example, if we run a React app on port 3000, we would want to expose port 3000 so we can use `3000-brevurl.brev.sh` to access `localhost:3000`.

Note: often there's a security layer built into the code (for example, user auth) so publicly exposing a port is not a security worry. If there _is_ a security concern with opening a port publicly, you can use the Brev CLI to port forward your Brev workspace port to your localhost. See below:

![Screenshot](media/brevportfwdlocalhost.png)
