# Authentication

The Madevo Assistant API uses token based authentication. Clients must authenticate using valid credentials to obtain an access token.

## Login

**Endpoint**  
POST /restapi/login

**Request Body**
```json
{
  "email": "user@example.com",
  "password": "yourpassword"
}

