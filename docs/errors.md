
# Errors and Status Codes

The Madevo Assistant REST API uses standard HTTP status codes to indicate whether a request was successful or resulted in an error. Error responses are designed to be clear and consistent to help clients diagnose issues quickly.

---

## Success Responses

| Status Code | Meaning |
|------------|---------|
| 200 | Request completed successfully |

---

## Client Errors

Client errors indicate that the request was invalid or could not be processed as sent.

| Status Code | Meaning |
|------------|---------|
| 400 | Bad request. The request payload or parameters are invalid |
| 401 | Unauthorized. Missing, expired, or invalid access token |
| 403 | Forbidden. The client does not have permission to access the resource |
| 404 | Not found. The requested endpoint or resource does not exist |

---

## Server Errors

Server errors indicate that the request was valid but could not be processed due to an internal issue.

| Status Code | Meaning |
|------------|---------|
| 500 | Internal server error |
| 502 | Bad gateway |
| 503 | Service unavailable |

---

## Error Response Format

When an error occurs, the API may return a JSON response describing the issue.

Example:

```json
{
  "error": "Unauthorized",
  "message": "Invalid or expired access token"
}
```

---

## Common Error Scenarios

### Invalid Authentication Token

- Access token is missing
- Access token has expired
- Access token is malformed

Resolution: Authenticate again or refresh the token.

---

### Invalid Request Payload

- Required fields are missing
- Field types are incorrect
- JSON payload is malformed

Resolution: Validate the request body against the endpoint documentation.

---

### Permission Denied

- User does not have access to the requested resource
- Action is not allowed for the current role

Resolution: Verify user permissions or contact the Madevo team.

---

## Best Practices for Error Handling

- Always check HTTP status codes
- Handle 401 responses by refreshing the access token
- Log error responses for troubleshooting
- Avoid retrying requests that return 4xx errors without modification

---

## Notes

- Error messages may vary depending on the endpoint
- Additional error details may be added in future API versions
```
