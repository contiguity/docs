# Receive Intents (Enterprise)
Your webhook endpoint can be configured in your Enterprise portal. It's the same URL to receive Intents, SMS, and iMessage.

`POST /your/webhook/url`

#### Parameters

- `code` (number): Recipient's phone number
- `message` (string): Content of the message received
- `type` (string, optional): Service type
- `crumbs` (object):
  - `from` (string): Your phone number
  - `to` (string): Customer's phone number
  - `id` (string): Your randomized ID.
  - `option` (number): The identifier you chose for the Message Intent

#### Forwarded Intent Format Example

```json
{
  "code": 200,
  "message": "Intent was selected by user",
  "crumbs": {
    "from": "+15555555555",
    "to": "+112552552555",
    "id": "vfxgtyrhnfgetwyeuyrkuti87ytdhfgxdfrw3",
    "option": "contact_rep"
  }
}
```

Contiguity expects a 200 response when sending webhook notifications.
