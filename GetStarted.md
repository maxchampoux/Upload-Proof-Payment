# ATTACH A DOCUMENT TO A PAYMENT #  

We may ask you to provide a proof of transaction under specific terms. You can anticipate our request and send us your invoice or the ID of the beneficiary to avoid any request from us and fully automate your payment process.
You document must be encoded with a base64 algorithm before to be sent.

## Encoding your document ##

The code below shows how to encode a file to send it along with the request:

```
$filename = "c:\\files\\somedoc.pdf" ;		//path of the file to send
$handle = fopen($filename, "rb");		//openning file in binary mode
$contents = fread($handle, filesize($filename));	//reading bytes from file
fclose($handle);				//closing file ressource
$toSend = base64_encode($contents);		//encoding the binary content with base64
```

## Route you must use ##

| Route | Description |
|-------|-------------|
| [`PUT /payments/-{id}/proofOfTransaction/`](#put_proofOfTransaction) | Attach a document to a payment (beta) |

## Details of the call ##

### <a id="put_proofOfTransaction"></a> Attach a document to a payment (beta) ###

```
Method: PUT
URL: /payments/-{id}/proofOfTransaction/
```

To send a file with this request, you have to extract the content of the file with a binary format, and encode it with a base64 algorithm to put in in the “file” field.
File size are limited to 8mo.

**Parameters:**

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| documentType | String | Required | The type of document to submit for a transaction. “invoice”. |
| invoice | String | Required | The name of the document to be attached. |
| file | String | Required | The binary content of the file, encoded with a base64 algorithm. |






