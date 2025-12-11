# Authentication

The Madevo Assistant API uses token based authentication. All protected endpoints require a valid access token.

## Login

Authenticates a user and returns an access token.

### Endpoint

POST /restapi/login

### Request Headers

Content-Type: application/json

### Request Body

```json
{
  "email": "user@example.com",
  "password": "yourpassword"
}
