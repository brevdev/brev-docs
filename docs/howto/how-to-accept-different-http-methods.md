# How To #6
## How to accept different HTTP Methods


To handle different http methods for a given url, create new functions named with the http request type you would like to handle. For example:


```python
def get()
    return {"message":"GET"}

def post()
    return {"message":"POST"}

def put()
    return {"message":"PUT"}

def delete()
    return {"message":"DELETE"}
```


Brev supports any of the following HTTP methods:

- get
- post
- put
- delete
- options
- head
- patch
- trace