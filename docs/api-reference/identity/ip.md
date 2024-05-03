# Contiguity Identity Services - IP Address

Contiguity provides an endpoint for looking up details associated with an IP address. CIS allows you to retrieve geographical and other relevant information, which can be used for fraud detection, localization, etc.

`POST /identity/lookup/ip`

### Parameters

- `ip` (string, required): The IP address to look up*

**Supported formats include dotted quad notation (IPv4), IPv6 colon notation, or a 32-bit unsigned integer (treated as an IPv4 address)*

#### Headers

- `Authorization`: Used for authentication. Specify it as `Token YOUR_TOKEN`.
- `Content-Type`: `application/json` or `application/x-www-form-urlencoded`

### Example Request

```bash
curl -X POST \
  -H "Authorization: Token YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "ip": "123.45.67.89"
}' \
  https://api.contiguity.co/identity/lookup/ip
```

### Response Format

The response is in JSON format and includes the following fields:

- `status` (number): HTTP status code.
- `message` (string): Result message.
- `crumbs` (object): Additional information about the IP address.

#### Crumbs Object

- `country` (string): Country associated with the IP address.
- `region` (string): Region associated with the IP address.
- `timezone` (string): Timezone of the IP address.
- `isInEU` (boolean): Indicates whether the IP address is located within the European Union (EU).
- `inDepth` (object): Additional detailed information.
  - `accuracy` (string): Accuracy of the location.
  - `city` (string): City associated with the IP address.
  - `coordinates` (object): Geographic coordinates.
    - `latitude` (float): Latitude of the IP address.
    - `longitude` (float): Longitude of the IP address.

### Example Response

```json
{
  "status": 200,
  "message": "IP successfully looked up",
  "crumbs": {
    "country": "United States",
    "region": "California",
    "timezone": "America/Los_Angeles",
    "isInEU": false,
    "inDepth": {
      "accuracy": "5",
      "city": "San Francisco",
      "coordinates": {
        "latitude": 37.7749,
        "longitude": -122.4194
      }
    }
  }
}
```

### Error Responses

- `400 Bad Request`: Missing or invalid parameters.
- `401 Unauthorized`: Invalid or suspended token provided, or ineligible account.
