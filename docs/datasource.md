# Data Ingestion

The Data Ingestion API allows clients to push structured data into a Madevo data source. This data can then be queried, analyzed, or used by AI assistants and agents within the Madevo platform.

---

## Push Data to Data Source

Insert one or more records into a specified data source.

### Endpoint

POST /restapi/datasource/insert

---

## Authentication

This endpoint requires authentication.

### Headers

Authorization: Bearer YOUR_ACCESS_TOKEN  
Content-Type: application/json

---

## Request Body

```json
{
  "datasource_id": "67890",
  "data": [
    {
      "timestamp": "2025-01-01T12:00:00Z",
      "metric": "temperature",
      "value": 22.5
    }
  ]
}
```

---

## Request Parameters

| Field | Type | Required | Description |
|------|------|----------|-------------|
| datasource_id | string | Yes | Identifier of the target data source |
| data | array | Yes | Array of records to insert |

---

## Data Format Guidelines

- Records must be valid JSON objects
- All records in a request should follow the same schema
- Timestamps should use ISO 8601 format in UTC
- Numeric values should use standard number types

---

## Response

```json
{
  "message": "Data successfully inserted"
}
```

---

## Response Fields

| Field | Type | Description |
|------|------|-------------|
| message | string | Confirmation of successful insertion |

---

## Batch Insertion

The API supports inserting multiple records in a single request.

Example:

```json
{
  "datasource_id": "67890",
  "data": [
    { "timestamp": "2025-01-01T10:00:00Z", "value": 21.2 },
    { "timestamp": "2025-01-01T11:00:00Z", "value": 21.9 },
    { "timestamp": "2025-01-01T12:00:00Z", "value": 22.5 }
  ]
}
```

---

## Error Responses

| Status Code | Meaning |
|------------|---------|
| 400 | Invalid request payload |
| 401 | Unauthorized or invalid token |
| 403 | Forbidden |
| 500 | Internal server error |

Error responses may include a descriptive message to assist debugging.

---

## Best Practices

- Validate data before sending
- Use consistent schemas per data source
- Batch records when possible to improve performance
- Monitor error responses during ingestion

---

## Notes

- Data validation rules depend on the configured data source
- Large payloads may be subject to size limits
- Ingestion behaviour may evolve in future API versions

