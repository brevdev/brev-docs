# Tutorial #1
## Make a backend for a todo list app.
Create tasks, get your tasks, and update them.


This tutorial will walk you through creating 3 APIs on Brev, hooked up to a database to store everything. If you find yourself stuck, wanna brainstorm anything, or just wanna chat, text us: 415-818-0207

The basic design:
- GET request to fetch all remaining todos
- POST request to create new todos
- PUT request to update a todo as completed


### 1: Create a new project
`note: you can skip this step if you want to use an existing Brev project`

Create a folder for this project. Go to that directory in your terminal, and initialize a Brev project.
```bash
brev init
```


### 2: Create the endpoint
In the directory of your brev project, create a new endpoint. We named it `todos` but you can name it however you like.
```bash
brev endpoint add --name todos
```
By default, everything with Brev is hosted and deployed for you! Run the below command to see the endpoint URLs.
```
brev endpoint list
```

Copy the URL and open it in a new tab with your web browser! You should see an empty response `{}`

Edit the endpoint file with your preferred code editor. You'll see a basic function called `get`. This is the function that gets called when the URL is hit via an HTTP GET request. 

### 3 Test the instantaneous deploy
Change the return of the `def get()` function, save the file, and refresh the URL in your browser tab. Everything is immediately available!

### 4 Create new tasks

We need to accept tasks to our function. We can send the tasks to our endpoint as JSON. Since Brev is built on top of FastAPI, we can leverage Pydantic BaseModel classes to represent our data. In the same file, above your `post` function, represent your JSON data as a BaseModel class:

```python
from pydantic import BaseModel

class ToDo(BaseModel):
    task: str
    status: str

```
Now that we've defined what a todo looks like, we just need to pass it in to our function. We should use a POST request since we're creating new data, so just create a new function called `post` in our endpoint file.

```python hl_lines="7 8"
from pydantic import BaseModel

class ToDo(BaseModel):
    task: str
    status: str

def post():
    return {}

```

Brev will automatically call the post function when the URL is hit with a POST request. Brev endpoint files are the entry points to your project.


To create a ToDo, simply pass in an instance of type `ToDo`. 

```python hl_lines="7"
from pydantic import BaseModel

class ToDo(BaseModel):
    task: str
    status: str

def post(todo: ToDo):
    return {}
```
Data validation happens automatically! So if your endpoint is called with JSON that doesn't include the `status` field, it'll return a `403` data validation error. You can comfortably expect your code to only execute if the required parameters are passed in.

Test it out! Run your endpoint using an app like Postman, the Brev console, or your terminal! Via the Brev CLI: 
```bash
brev endpoint run --name todo --method POST --body '{"task":"Brev Tutorial 1", "status": "incomplete"}'
```


### 5 Save the tasks in a database
Brev comes with a database out of the box. Simply import it to use it!

```python hl_lines="1 8"
from global_storage import storage_context
from pydantic import BaseModel

class ToDo(BaseModel):
    task: str
    status: str

def post(todo: ToDo, db=storage_context("todos")):
    return {}
```

We're passing an instance of the database to the post function. By giving it the context name "todos", Brev will look for the database table named `todos`, or create it if it doesn't exist -- no initialization needed! :)

Now that we have a database set up, let's store the todos, and return a useful message.

```python hl_lines="1 10"
from global_storage import storage_context
from pydantic import BaseModel
import uuid

class ToDo(BaseModel):
    task: str
    status: str

def post(todo: ToDo, db=storage_context("todos")):
    db[uuid.uuid4()] = todo # save the todo
    return {"success": f"Successfully saved task {todo.task}" }
```

From the Brev dev console, go to the storage viewer to see your database items!

### 6 Get your active todos

Storing is no fun if we can't access everything. Create a GET request that returns your active todos, first passing the database context to your get function.

```python hl_lines="13 14 15"
from global_storage import storage_context
from pydantic import BaseModel
import uuid

class ToDo(BaseModel):
    task: str
    status: str

def post(todo: ToDo, db=storage_context("todos")):
    db[uuid.uuid4()] = todo # save the todo
    return {"success": f"Successfully saved task {todo.task}" }

def get(db=storage_context("todos")):
    pending_todos = [todo for todo in db.values() if todo.status=="pending"]
    return {"result": pending_todos}
```


### 7 The final step is to create an endpoint to modify 

We want to edit a specific ToDo and mark it as completed. Given a todo ID, we can make a PUT request to change it's state.

Add a function for a put request that accepts the ID as a query parameter. (Don't forget to pass the db in as well  )
```python hl_lines="17 18"
from global_storage import storage_context
from pydantic import BaseModel
import uuid

class ToDo(BaseModel):
    task: str
    status: str

def post(todo: ToDo, db=storage_context("todos")):
    db[uuid.uuid4()] = todo # save the todo
    return {"success": f"Successfully saved task {todo.task}" }

def get(db=storage_context("todos")):
    pending_todos = [todo for todo in db.values() if todo.status=="pending"]
    return {"result": pending_todos}

def put(id, db=storage_context("todos")):
    return {}
```
The incoming data to a function can be a variety of types. Using a BaseModel type like we do for the POST request is what specifies incoming data as JSON. 

Final step is to just pop the associated id
```python hl_lines="17 18"
from global_storage import storage_context
from pydantic import BaseModel
import uuid

class ToDo(BaseModel):
    task: str
    status: str

def post(todo: ToDo, db=storage_context("todos")):
    db[uuid.uuid4()] = todo # save the todo
    return {"success": f"Successfully saved task {todo.task}" }

def get(db=storage_context("todos")):
    pending_todos = [todo for todo in db.values() if todo.status=="pending"]
    return {"result": pending_todos}

def put(id, db=storage_context("todos")):
    db[id]['status'] = "completed"
    return {"result": }
```

And there you have it! You now have everything you need to build out a ToDo app! Brev is meant to be configured to your specific use case. 

### Further Reading

- [How To: Best Practices for Brev DB](../../discussions/best-practices-for-brev-database)

<!-- - [Tutorial #2: Make SMS bot w/ Twilio](index.md) -->