# How To #8
## How to pass request files to your endpoints


To receive files sent as form data you can declare an argument with default value of `File(...)`.


```python
from fastapi import File

def post(file_contents: bytes = File(...)):

  return {}
```

We can use Brev's built in [file upload function](../../reference/out-of-the-box-sms-file-upload-roboflow/#file-upload) to save the file and return a link to it!

```python hl_lines="2 6 8"
from fastapi import File
import file_storage

def post(file_contents: bytes = File(...)):

  link = file_storage.upload(file_contents)

  return {"file_url": link}
```


