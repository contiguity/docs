# Generate a Message Intent (Enterprise-only)

Contiguity Message Intents is a service designed to replicate the Apple For Business experience at a fraction of the cost. It works by utilizing special URLs hosted by Contiguity, and special iMessage infrastructure to load previews that imitate buttons.

`POST /enterprise/message/generate`

### Parameters

- `toNumber` (string, required): The recipient's phone number.
- `fromNumber` (string, required): The sender's phone number. This is important, as Message Intents will reopen the conversation to this number after an option is selected.
- `embedText` (string, required): The Message Intent's title. This should be fairly short.
- `imageURL` (string, required): A URL pointing to an image. The image must be less than 150px by 150px (149px * 149px works best) to render a button/pill looking Message Intent.
- `companyName` (string, required): Your company's name.
- `option` (string, required): Identify this Message Intent (i.e "contact_agent") in your backend.


#### Headers

- `Authorization`: Used for authentication. Specify it as `Token YOUR_TOKEN`.
- `Content-Type`: `application/json` or `application/x-www-form-urlencoded`

### Example Request

```bash
curl -X POST \
  -H "Authorization: Token YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "toNumber": "+1234567890",
    "fromNumber": "+0987654321",
    "embedText": "Contact a representative",
    "imageURL": "https://example.com/image.jpg?w=149px&h=149px",
    "companyName": "Twilio",
    "option": "contact_rep"
}' \
  https://api.yourdomain.com/enterprise/message/generate
```

### Response Format

The response is in JSON and includes the following fields:

- `code` (number): HTTP status code.
- `message` (string): Result message.
- `url` (string): The generated message intent URL.
- `options` (object): Additional information about the generated intent.

#### Options Object

- `name` (string): Company name.
- `to` (string): Recipient's phone number.
- `from` (string): Sender's phone number.
- `id` (string): Public key associated with the token.
- `option` (string): Additional options provided.


### Example Response
```json
{
  "code": 200,
  "message": "Generated Message Intent",
  "url": "https://api.contiguity.co/enterprise/message/intent?id=xxxxxx&fromNumber=string&toNumber=string&companyName=Twilio&option=text&embedText=title&imageURL=image",
  "options": {
    "name": "Twilio",
    "to": "string",
    "from": "string",
    "id": "f033895f34162765431fba4259bc42b7fcf",
    "option": "contact_rep"
  }
}
```

### Error Responses

- `400 Bad Request`: Missing or invalid parameters.
- `401 Unauthorized`: Invalid or suspended token provided, or ineligible account.
