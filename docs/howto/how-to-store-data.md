# How To #7
## How to Store Data


You probably want to persist data in a database. Brev's built in database is great for simple applications, or you can fully configure your own database if your use case demands it. Brev's db is a key-value, nosql database. Check out our [discussion about how to best utilize Brev DB in your application.](../discussions/best-practices-for-brev-database.md)



You can fully configure your own database, or use the built in Brev DB. 


Import global_storage:

```python
from global_storage import storage_context
```

This is the database object. Pass in a reference to the table you want. Brev will automatically create and configure it for you.


```python hl_lines="3"
from global_storage import storage_context

def get(db=storage_context("my_items")):
    ...
```

This passes a reference to the table `my_items`, and creates the table first if needed. It interfaces a lot like a python dictionary.

```python hl_lines="4"
from global_storage import storage_context

def get(db=storage_context("my_items")):
    db[key] = value # store an item
    ...
```

You can read more about the storage_context [here](../reference/built-in-database-storage-context.md).