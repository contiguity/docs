# Send iMessage (Enterprise-only)
As long as you provided Contiguity a valid token, and provide valid inputs, sending iMessages will be a breeze. You can manage iMessage nodes in the Enterprise Portal.

?> Note: Contiguity expects the recipient phone number to be formatted in E.164. You can attempt to pass numbers in formats like NANP, and the SDKs will try their best to convert it. The API will also attempt to do so. If conversion fails, it will throw an error! 

!> iMessage is an international messaging solution. Country codes (+1, +44, +7, etc) are important and required.

`POST /send/text`

#### Parameters

- `to` (string, required): Recipient's phone number.
- `message` (string, required): Content of the message.
- `beta_features` (map, required): Enable iMessage, 'from', and Fallback
  - `from` (string, optional): Provide the number you'd like to send from (iMessage)
  - `imessage` (boolean, required): Enable iMessage
  - `fallback` (boolean, optional): Should Contiguity send your message via SMS if iMessage fails?

#### Headers

- `Authorization`: Used for authentication, specify it as `Token YOUR_TOKEN`
- `Content-Type`: `application/json` or `application/x-www-form-urlencoded`

#### Example request
```bash
curl -X POST https://api.contiguity.co/send/text \
  -H "Authorization: Token YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "to": "+1234567890",
    "message": "Hello, this is a test iMessage.",
    "beta_features": {
      "imessage": true,
      "fallback": false
    }
  }'
```

#### Response Format

- `message` (string): Result message.
- `crumbs` (object): Additional request info.

#### Example Response

```json
{
  "message": "Successfully sent",
  "crumbs": {
    "plan": "unlimited",
    "quota": 12,
    "type": "imessage",
    "ad": false
  }
}
```

#### Error Responses

- `400 Bad Request`: Missing parameters.
- `401 Unauthorized`: Invalid or suspended token.
- `500 Internal Server Error`: Sending failed or internal errors occurred.