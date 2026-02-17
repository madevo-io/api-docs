# Authentication

The Madevo API uses token-based authentication.  
All protected endpoints require a valid access token.

Authentication ensures secure access to assistant interactions and datasource operations.

---

# Authentication Flow

1. Authenticate using email and password  
2. Receive an access token  
3. Include the token in the `Authorization` header  
4. Refresh the token when it expires  

---

# Login

Authenticate a user and obtain an access token.

## Endpoint

```
POST /restapi/login
```

## Headers

```
Content-Type: application/json
```

## Request Body

```json
{
  "email": "user@example.com",
  "password": "yourpassword"
}
```

## Request Parameters

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| email | string | Yes | User email address |
| password | string | Yes | User password |

## Response

```json
{
  "token": "your_access_token"
}
```

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| token | string | Access token used for authenticated requests |

---

# Refresh Token

Generate a new access token using an existing valid or recently expired token.

## Endpoint

```
POST /restapi/refresh-token
```

## Headers

```
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

## Request Body

```json
{}
```

## Response

```json
{
  "token": "new_access_token"
}
```

---

# Using the Access Token

Include the access token in the `Authorization` header for all protected endpoints.

```
Authorization: Bearer YOUR_ACCESS_TOKEN
```

Requests without a valid token will return:

```
401 Unauthorized
```

---

# Token Behaviour

- Tokens have a limited lifetime  
- Expired or invalid tokens return a `401` response  
- Clients must refresh tokens before retrying protected requests  
- After refreshing, replace the old token immediately  
- Do not retry requests with an expired token  

---

# Recommended Token Handling Strategy

For production systems:

1. Detect `401 Unauthorized` responses  
2. Call `/restapi/refresh-token`  
3. Retry the original request with the new token  
4. If refresh fails, re-authenticate using login  

Avoid repeated retries with invalid credentials.

---

# Error Responses

| Status Code | Meaning |
|------------|---------|
| 400 | Invalid request payload |
| 401 | Unauthorized or invalid credentials |
| 403 | Forbidden |
| 500 | Internal server error |

Example error response:

```json
{
  "error": "unauthorized",
  "message": "Invalid or expired access token"
}
```

---

# Security Best Practices

- Never expose passwords in frontend applications  
- Perform authentication from a secure backend service  
- Store tokens securely  
- Always use HTTPS  
- Avoid logging tokens or authentication payloads  
- Rotate credentials if compromise is suspected  

---

# Notes

- Token lifetime and behavior may evolve in future API versions  
- Authentication requirements depend on user permissions  
- Access to datasources and assistant features is permission-based  
