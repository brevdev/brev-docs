# How To #3
## Read Print Statements Outside of Brev CLI or Console

Executing any of your endpoints using the enpoint runner in the console or through the CLI (`run` command) will display your print statements. If you want to view the stdout in a different environment, for example, in a react front end app, we've made it available in the header. 

Look for the `x-stdout` header in the networks tab or print it out. Note: it will be URL encoded.

`x-stdout: %5Bprint%5D%20%5Bendpoint.websiteForm.get%3A8%5D%20hey%20from%20brev%0A`