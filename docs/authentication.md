# Authentication

The Madevo Assistant API uses token based authentication to secure access to all protected endpoints. Clients must authenticate using valid user credentials to obtain an access token. This token must be included in the Authorization header for all subsequent API requests.

---

## Authentication Flow

1. Authenticate using email and password to obtain an access token  
2. Include the access token in the Authorization header for protected endpoints  
3. Refresh the access token when it expires  

---

## Login

Authenticates a user and returns an access token.

### Endpoint

POST /restapi/login

---

## Request Headers

Content-Type: application/json

yaml
Copy code

---

## Request Body

```json
{
  "email": "user@example.com",
  "password": "yourpassword"
}
Request Parameters
Field	Type	Required	Description
email	string	Yes	User email address
password	string	Yes	User password

Response
json
Copy code
{
  "token": "your_access_token"
}
Response Fields
Field	Type	Description
token	string	Access token used for authenticated requests

Refresh Token
Generates a new access token using an existing valid or recently expired token.

Endpoint
POST /restapi/refresh-token

Authentication
This endpoint requires an existing access token.

Required Headers
pgsql
Copy code
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
Request Body
json
Copy code
{}
Response
json
Copy code
{
  "token": "new_access_token"
}
Token Usage
All protected endpoints require the Authorization header to be set as follows:

makefile
Copy code
Authorization: Bearer YOUR_ACCESS_TOKEN
Token Expiry and Refresh
Access tokens have a limited lifetime

Clients should refresh tokens before or after expiration

After refreshing, the new token should replace the previous one

Requests made with expired or invalid tokens will return a 401 response

Error Responses
Status Code	Meaning
400	Invalid request payload
401	Unauthorized or invalid credentials
403	Access forbidden
500	Internal server error

Error responses typically include a descriptive message to assist with debugging.

Security Best Practices
Never expose user passwords in client side code

Always store access tokens securely

Use HTTPS for all API requests

Rotate tokens regularly

Avoid logging sensitive authentication data

