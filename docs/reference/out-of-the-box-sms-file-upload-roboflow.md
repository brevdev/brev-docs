# Out-of-the-Box Functionality

Brev comes with built in tools to make it easier to focus on building, not configuring.


## SMS
Use the built in SMS messenger to send text messages from any endpoints. This is a great way to develop your prototype and see how quickly you can build a real application with Brev, however, you might be better off setting up Twilio for heavy production use cases.

The built-in SMS comes from a real 10-digit number (not a short code). An exception will be thrown if the message fails to send. 
Simply `import sms` from a file in a Brev project. The API is 

```python
sms.send(phone_number: str, message: str)
```

Here's a full example:

```python
import sms

sms.send("415555555", "hello from Brev!")
```

## File Upload

Often you want to store files like images, videos, docs, or arbitrary binary data. Use `import file_storage` to upload data. A long unique link containing the file will be returned.

Note: anyone with access to the link will have access to the file, and the link does not expire.


```python
file_storage.upload(data: Union[bytes, BinaryIO], content_type: Optional[str] = None, content_disposition: Optional[str] = None, content_encoding: Optional[str] = None) -> str
```

|  Parameters                            |                                      |
| :------------------------------------  | :----------------------------------- |
| data                 | A file like object or bytes can be used. |
| content_type         | An optional string to specify the [file media type](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types). Specifying the correct type allows browsers do download the file correctly.    |
| content_disposition  | An optional string to specify the [content disposition](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Disposition). This tells browsers if it should treat the file as part of a webpage or as a downloadable attachement. |
| content_encoding     | an optional string to specify the [content encoding](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Encoding). |
| Returns | Returns a complete url with a long unique id. Anyone who has access to this link has access to the file. |


## Roboflow

If you have a [Roboflow](https://roboflow.com/) computer vision model, you can infer your model with `import roboflow`.

```python
roboflow.infer(
    model_id: str,
    image_base64: str,
    format: Union[roboflow.Format, str] = roboflow.Format.json,
    access_token: Optional[str] = None,
) -> requests.Response
```


|  Parameters                            |                                      |
| :------------------------------------  | :----------------------------------- |
| model_id        | A file like object or bytes can be used. |
| image_base64    | The image data in base64.    |
| format          | A roboflow.Format type or string "json", "image" |
| access_token    | The optional roboflow access token. If not provided here, `ROBOFLOW_ACCESS_TOKEN` must be set as an environment variable. |
| Returns | The requests.Response from the https://infer.roboflow.ai/{model} endpoint. ([See request libarary](https://requests.readthedocs.io/en/master/)) |



The following enum
```python
roboflow.Format: Enum
```
has values:

  - json = "json"
  - image = "image"