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


**Example: Attach a document to a payment (beta) **
```js
POST /payments/OTg3NTg/proofOfTransaction/
{
    "documentType": "Invoice",
    "tag": "toto",
    "file": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAMAAAAoLQ9TAAAABGdBTUEAANbY1E9YMgAAABl0RVh0U29mdHdhcmUAQWRvYmUgSW1hZ2VSZWFkeXHJZTwAAAGAUExURQxS1ISawgBGyebt+VZ6vmGK1miV58bO3O3u8gRJykV31E170brM7RNSyXuRukJ64jNkvl2H1Xmh6wFK0fT19+vw++rs8QFGxlt/xOLm7KOwylSB01l7urbB1LW/0lJ/0py25vDw8+ju+oucv9PZ4yJezUh40oOo7zJpzSljzV6I1lmE1Ep50e7z/PDx9Ky4zfb2+JOt3FF+0hlc2AlLxjxvzUFptEd406+60EZ73NTf9EhxvWGP5XeOuixm0z9x0HeQvSxlzVB90xZZ1h5d0unr7+7w85qx3s/V4Stgwo+x8bnC1b/I2Vp6tliC0ViD1H6ZzF6G0UyD6GSAtVB+1Chm2drf5yVgzZy68kh931F6xlR/zuDp+tbg9N/o+l6Bw8HJ2iFk4DRw4YCWv0p601KF5V6P6T9puW+Ku4qewnCIt3iOuE980WSL0iVk2Stfvixo1jlz3Vt9vl5+uk11wPPz9VyDzAhO0MnQ3S5lyYeg0FB90aG+80l40Nzg6P///xIhGr0AAACAdFJOU/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////8AOAVLZwAAAPdJREFUeNpiqAcBPRVvWQ8OMJMBiEXkbIvjJWSy9PUgAmLKRYFarKzafix8kiABA2UJQW1WHh5BeemobA6ggByLv7Q8a6yVIDc3d4lUPUMpX7SRUXUOqxa3jo5abbArQ5ivEze3jqCCQoiGo2Z4OjsDO0sKl72GuaiSpri4OFO+BQO7tSqvibgqM7MLExB4WjDUmXGKM3HaKSkVlAsLCwtUMIhk8HIyuFiKikbmGTMwyIgx1MsKOIcW2ujqsvEnJVZKgRzGaMqfKhQXo54WxOXgBnZ6ZhmbekSNl1BusiTUc7KMAYbuVYwWUM8BgaJKgo8KxPsAAQYAJwc98FQAQqUAAAAASUVORK5CYII="
}

```
**Return:**
| Field | Type | Description |
|-------|------|-------------|
| payment | [Payment Object](../objects/objects.md#payment_object) | An encoded JSON body advising the modification on payment status. |

```js
{
  "id": "Na5Dv6E",
  "status": "planified",
  "createdDate": "2016-01-01 00:00:00",
  "desiredExecutionDate": "2016-01-01",
  "executionDate": "2016-01-01",
  "amount": {
    "value": "2.257",
    "currency": "USD"
  },
  "counterValue": {
    "value": "2.257",
    "currency": "USD"
  },
  "rate": {
    "currencyPair": "EURUSD",
    "midMarket": "2.257",
    "date": "2016-01-01 00:00:00",
    "coreAsk": "2.257",
    "coreBid": "2.257",
    "appliedAsk": "2.257",
    "appliedBid": "2.257"
  },
  "tag": "string",
  "externalBankAccountId": "Na5Dv6E",
  "sourceWalletId": "Na5Dv6E",
  "communication": "string",
  "priorityPaymentOption": "normal",
  "feePaymentOption": "BEN"
}
```
