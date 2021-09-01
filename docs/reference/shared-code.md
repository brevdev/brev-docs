# Shared Code

You'll notice each project comes with a singular shared code file. The endpoint handlers are defined in your endpoints, but shared logic, such as common functions or classes, can go in shared code. 

You can access the shared code by importing `shared` in any endpoint. So the following will return pancakes

```python
import shared

def get():
  return {"breakfast": shared.breakfast}  # {"breakfast": "pancakes"}
```

The next version of Brev will expand this concept, letting you have a more custom file structure. 
