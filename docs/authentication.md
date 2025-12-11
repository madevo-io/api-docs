# Authentication

The Madevo Assistant API uses token based authentication. All protected endpoints require a valid access token.

---

## Authentication Flow

1. Authenticate using email and password
2. Receive an access token
3. Include the token in the Authorization header
4. Refresh the token when it expires

---

## Login

Authenticate a user and obtain an access token.

### Endpoint

POST /restapi/login

### Headers

Content-Type: application/json

### Request Body

```json
{
  "email": "user@example.com",
  "password": "yourpassword"
}
```

### Request Parameters

| Field | Type | Required | Description |
|------|------|----------|-------------|
| email | string | Yes | User email address |
| password | string | Yes | User password |

### Response

```json
{
  "token": "your_access_token"
}
```

### Response Fields

| Field | Type | Description |
|------|------|-------------|
| token | string | Access token used for authenticated requests |

---

## Refresh Token

Generate a new access token using an existing valid or recently expired token.

### Endpoint

POST /restapi/refresh-token

### Headers

Authorization: Bearer YOUR_ACCESS_TOKEN  
Content-Type: application/json

### Request Body

```json
{}
```

### Response

```json
{
  "token": "new_access_token"
}
```

---

## Using the Access Token

Include the access token in the Authorization header for all protected endpoints.

```text
Authorization: Bearer YOUR_ACCESS_TOKEN
```

---

## Token Behaviour

- Tokens have a limited lifetime
- Expired tokens return a 401 response
- Refresh tokens before or after expiration
- Replace the old token after refreshing

---

## Error Responses

| Status Code | Meaning |
|------------|---------|
| 400 | Invalid request payload |
| 401 | Unauthorized or invalid credentials |
| 403 | Forbidden |
| 500 | Internal server error |

Error responses may include a descriptive message to assist debugging.

---

## Security Best Practices

- Never expose passwords in frontend code
- Store tokens securely
- Always use HTTPS
- Avoid logging authentication data

---

## Notes

- Token lifetime and behaviour may change in future API versions
- Authentication requirements depend on user permissions
