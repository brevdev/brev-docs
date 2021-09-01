# How To #2
## How To Add JSON Body

Query parameters can be used for simple variables, but often you'll have more complex data to send to API, or you want it sent over more securely, rather than as part of the URL. We can do this by sending our data as a JSON object. 

The JSON object can hold anything, so we need to define the data before passing to a Brev function. Defining the data allows the automatic validation to take place, so your code only gets executed if the proper inputs were received.

### 1: Define the data with pydantic BaseModel class
```python
from pydantic import BaseModel

class MyJsonBody(BaseModel):
    best_tv_show_ever: str
    does_kel_love_orange_soda: bool
```


### 2: Pass an instance of the class to the function
```python  hl_lines="8"
from pydantic import BaseModel

class MyJsonBody(BaseModel):
    best_tv_show_ever: str
    does_kel_love_orange_soda: bool

def get(incoming: MyJsonBody):
    return {"result": incoming.does_kel_love_orange_soda}
```

That's it! You can now access the incoming JSON as an instance of your pydantic class!
