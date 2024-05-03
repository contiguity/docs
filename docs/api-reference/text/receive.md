
# Receive texts (Enterprise)
Contiguity Enterprise customers who lease Text or iMessage nodes can optionally receive messages, which are forwarded by Contiguity to your application via simple HTTP POST requests.

Your webhook endpoint can be configured in your Enterprise portal.

`POST /your/webhook/url`

#### Parameters

- `code` (number): Recipient's phone number
- `message` (string): Content of the message received
- `type` (string, optional): Service type
- `crumbs` (object):
  - `from` (string): Sender's phone number
  - `to` (string): Your phone number
  - `message` (string): Sender's message content
  - `time` (number): Unix timestamp

#### Forwarded Message (Text) Format Example

```json
{
  "code": 200,
  "message": "Incoming message received",
  "crumbs": {
    "from": "+15555555555",
    "to": "+112552552555",
    "message": "how's it going?",
    "time": 1713601200
  }
}
```

Contiguity expects a 200 response when sending webhook notifications.

#### Forwarded Message (iMessage) Format Example

```json
{
  "code": 200,
  "message": "Incoming message received",
  "crumbs": {
    "from": "+15555555555",
    "to": "+112552552555",
    "message": "how's it going?",
    "time": 1713601200
  },
  "type": "imessage"
}
```

**Contiguity will soon allow seperate webhooks for iMessage & SMS/RCS**