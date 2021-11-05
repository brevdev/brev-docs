# How To
## Make a port public

If you're accessing your localhost url such as `3000-jelly-brevdev.brev.sh`, you'll notice it requires your password.

If you want to remove auth to use Postman, consume the endpoint in your frontend, or just show your mom what you built, you can do so in the `.brev/ports.yaml` added to every Brev workspace.

![Screenshot](media/ports.png)

Add the port you wish to expose in the list and that's it!

**Note:** the version field is optional. It could be useful if you choose to commit this to your project repo.