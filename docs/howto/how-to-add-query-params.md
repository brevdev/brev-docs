# How To #1
## How To Add Query Params

Query parameters are variables encoded in the URL of your API/endpoint. For example `https://slug.brev.dev/api/test?greeting=hola`

In this case, `greeting` is the variable, and `hola` is the value of `greeting`. 

To use this in an endpoint on Brev, simply pass the variable name into your function. For example, for the above call, the following function

```python
def get(greeting)
    return {"greeting": f"{greeting}"}
```

would return 

```json
{
    "greeting": "hola"
}
```


