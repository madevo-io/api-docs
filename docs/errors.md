# Errors and Status Codes

The Madevo REST API uses standard HTTP status codes to indicate whether a request was successful or resulted in an error.

Error responses are designed to be structured, consistent, and machine-readable to support automation workflows and production integrations.

---

# Success Responses

| Status Code | Meaning |
|------------|---------|
| 200 | Request completed successfully |

---

# Client Errors (4xx)

Client errors indicate that the request was invalid, incomplete, unauthorized, or could not be processed as sent.

| Status Code | Meaning |
|------------|---------|
| 400 | Bad request. The payload or parameters are invalid |
| 401 | Unauthorized. Missing, expired, or invalid access token |
| 403 | Forbidden. The client does not have permission to access the resource |
| 404 | Not found. The requested endpoint or resource does not exist |
| 409 | Conflict. Request conflicts with current resource state |
| 422 | Unprocessable entity. Request is valid but fails validation rules |
| 429 | Too many requests. Rate limit exceeded |

---

# Server Errors (5xx)

Server errors indicate that the request was valid but could not be processed due to an internal or upstream issue.

| Status Code | Meaning |
|------------|---------|
| 500 | Internal server error |
| 502 | Bad gateway |
| 503 | Service unavailable |
| 504 | Gateway timeout |

---

# Error Response Format

When an error occurs, the API may return a structured JSON response describing the issue.

Example:

```json
{
  "error": "unauthorized",
  "message": "Invalid or expired access token"
}
```

### Standard Error Fields

| Field | Type | Description |
|-------|------|-------------|
| error | string | Machine-readable error identifier |
| message | string | Human-readable description of the issue |

Additional fields may be included depending on the endpoint.

---

# Assistant-Specific Error Scenarios

The Assistant endpoint may introduce additional validation or response-related errors.

## Invalid JSON Response (Automation Workflows)

If a strict JSON-only response was requested and the assistant output does not match the specified schema, clients may detect a validation failure.

Example:

```json
{
  "error": "invalid_json_response",
  "message": "Assistant response did not match requested schema."
}
```

Recommended handling:

- Validate JSON structure before execution  
- Retry once with stricter prompt instructions  
- Escalate to manual review if validation continues to fail  

---

## Rate Limiting (429)

If request volume exceeds allowed thresholds, the API may return:

```
429 Too Many Requests
```

Recommended handling:

- Implement exponential backoff  
- Avoid parallel requests using the same conversation_id  
- Throttle high-frequency automation tasks  

---

## Timeout Handling (504)

A 504 status indicates that the request timed out while waiting for an upstream response.

Recommended handling:

- Retry using the same conversation_id  
- Reuse the exact same request payload  
- Avoid modifying the prompt during retry  

---

# Common Error Scenarios

## Invalid Authentication Token

Possible causes:

- Access token is missing  
- Access token has expired  
- Access token is malformed  

Resolution:

- Refresh the token using the authentication flow  
- Retry the request with a valid token  

---

## Invalid Request Payload

Possible causes:

- Required fields are missing  
- Field types are incorrect  
- JSON payload is malformed  

Resolution:

- Validate the request body against the endpoint documentation  
- Ensure required parameters are present  

---

## Permission Denied (403)

Possible causes:

- User does not have access to the requested resource  
- Action is not allowed for the current role  
- Datasource permissions restrict access  

Resolution:

- Verify user permissions  
- Confirm resource ownership and access rights  

---

# Best Practices for Error Handling

- Always check HTTP status codes before processing responses  
- Handle 401 responses by refreshing the access token  
- Do not retry 4xx errors without modifying the request  
- Implement exponential backoff for 5xx and 429 errors  
- Log request and response pairs for traceability  
- Validate structured outputs before triggering automation actions  

---

# Notes

- Error messages may vary depending on the endpoint  
- Additional error fields may be introduced in future API versions  
- Clients should not rely on exact wording of error messages, only on status codes and structured fields  
