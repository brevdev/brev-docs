# How To # 10

## How to Save a File

You can save a file using Brev's built in [file upload function](../../reference/out-of-the-box-sms-file-upload-roboflow/#file-upload).

```python hl_lines="7"
from fastapi import File
import file_storage

def post()
#   file_contents = ...

  link = file_storage.upload(file_contents)

  return {"file_url": link}
```

The file upload function `.upload()` returns a URL to your file. You can store that URL in your Brev DB or simply return it from your endpoint! The URL does not expire.

See how to upload files to your endpoints [here](../how-to-pass-request-files-to-endpoints).
