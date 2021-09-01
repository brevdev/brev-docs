# How To #4
## How To Add Environment Variables

You can add environment variables to any Brev endpoint. It's a good practice to avoid using secret keys and other system level variables directly in the code. 



=== "CLI"

    From the CLI, use the `add` command on the `env` resource:

    `brev env add --name MY_SECRET_KEY`

    This will prompt you to enter the value, and that's it! 


=== "Console"

    Open the environment variables (.env) from the button bar, add the variable name and value, click `add variable`! 

    ![Screenshot](media/variables.png)
    

**Note:** these variables are protected per project. The variable value is encrypted and we don't support changing it. However, you can always delete it and add it back again with a different value. 

Freely use the variable in your code, insuring variables is imported:

```python
import variables

def get():
    print(f"Secret Key: {variables.MY_SECRET_KEY}")
    return{}
```

Doing this will make your code more secure, since the secret keys are encrypted and not pushed as part of your code. Additionally, your code will be cleaner since changing this variable only needs to happen in one place, no matter how often you use the variable.

