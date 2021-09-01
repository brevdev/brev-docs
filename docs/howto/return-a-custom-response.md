# How To #9

## How to return a custom response

Http responses are used to send data back to the client. Responses include a body, headers, cookies, and a status code.

As you have seen, you can create a response by returning from an endpoint handler. By default the response status code is 200. The object returned will be used as the body.

```python
def post():
    return {"return": True} # returns 200
```

To return a custom response you can return a [Starlette response object](https://www.starlette.io/responses/).

Simply import `JSONResponse` and return that instead.

```python
from fastapi.responses import JSONResponse

def post():
  return JSONResponse(status_code=201, content={"message": "created"})
```