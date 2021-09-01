# Reference

Brev is built on top of FastApi/ (v0.61.0) Starlette and supports much of its API. To dig deeper in request/response, validation and documenation it might be helpful to checkout their docs.

Brev lets you create projects. In each project, you'll find:

- Endpoints: Code that responds to http requests.
- Shared Code: Code that can be shared by any endpoint in a project
- Packages: Installable 3rd party packages from PyPi that can be used in endpoints or shared code
- Variables: A secure way to use and manage secrets, keys, passwords and is also a good way to manage environment variables or global constants in your code.
- Storage: A simple key value database. It can be thought of as a persistent dictionary accross requests as its api closely mirrors python's native dict type. It's a great way to build a proof of concept without needing to hook up a database.

####Below are full references for Brev components.

### [Brev DB (storage_context)](built-in-database-storage-context.md)
The built-in Brev DB, imported as `storage_context`

### [Shared Code](shared-code.md)
Write code accessible by all of your endpoints.

### [Environment Variables](env-secrets-manager.md)
Use Brev's built-in encrypted secrets/environment variable manager rather than putting your secrets in plain text.

### [Out-of-the-Box Functionality](out-of-the-box-sms-file-upload-roboflow.md)
Send SMS text messages, save upload files, and run computer vision inference without any additional setup!

### [Runtime and Environment](runtime-and-environment.md)
Learn more about your Brev server's runtime and environment.

### [Limitations](limitations.md)
Understand what limitations exist within a Brev deploy and applicable workarounds.
