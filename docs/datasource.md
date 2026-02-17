# Data Ingestion

The Data Ingestion API allows clients to push structured data into a Madevo datasource.

Ingested data can then be:

- Queried via API  
- Analyzed by AI assistants  
- Used in automation workflows  
- Visualized in dashboards  
- Processed by agents  

Datasources form the foundation of operational intelligence within the Madevo platform.

---

# Push Data to Datasource

Insert one or more records into a specified datasource.

## Endpoint

```
POST /restapi/datasource/insert
```

---

# Authentication

This endpoint requires authentication.

## Headers

```
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

---

# Request Body

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

# Request Parameters

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| datasource_id | string | Yes | Identifier of the target datasource |
| data | array | Yes | Array of records to insert |

---

# Data Format Guidelines

To ensure consistent querying and assistant reasoning:

- Records must be valid JSON objects  
- All records in a single request should follow the same schema  
- Timestamps must use ISO 8601 format in UTC  
- Numeric values must use standard JSON number types  
- Avoid mixing incompatible field types within the same datasource  

Consistent schemas significantly improve assistant analysis quality.

---

# Timestamp Requirements

All timestamps must be provided in ISO 8601 format using UTC.

Example:

```
2025-01-01T12:00:00Z
```

If timestamps are omitted, ingestion may fail depending on datasource configuration.

---

# Response

```json
{
  "message": "Data successfully inserted"
}
```

---

# Response Fields

| Field | Type | Description |
|-------|------|-------------|
| message | string | Confirmation of successful insertion |

---

# Batch Insertion

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

Batch insertion is recommended for:

- High frequency telemetry  
- Sensor pipelines  
- Event streams  
- Periodic aggregation jobs  

---

# Assistant and Datasource Context

Assistant responses depend on the data available within connected datasources.

Important considerations:

- Assistant outputs vary based on datasource content  
- User permissions determine accessible datasources  
- Live datasources may change between requests  
- Historical queries depend on accurate timestamps  

For deterministic analysis, ensure:

- Clear time boundaries in assistant prompts  
- Consistent schema usage  
- Reliable timestamp formatting  

---

# Idempotency and Ingestion Strategy

For production pipelines:

- Avoid sending duplicate records  
- Use deterministic timestamps  
- Ensure retry logic does not reinsert identical payloads  

If retrying ingestion after a network failure, confirm whether the previous request was committed.

---

# Error Responses

| Status Code | Meaning |
|------------|---------|
| 400 | Invalid request payload |
| 401 | Unauthorized or invalid token |
| 403 | Forbidden |
| 409 | Conflict with existing data |
| 422 | Validation failed |
| 429 | Rate limit exceeded |
| 500 | Internal server error |
| 503 | Service unavailable |

Example error response:

```json
{
  "error": "validation_error",
  "message": "Invalid timestamp format"
}
```

---

# Best Practices

- Validate data before sending  
- Use consistent schemas per datasource  
- Batch records when possible to improve performance  
- Implement retry logic with exponential backoff  
- Log ingestion results for traceability  
- Monitor 4xx and 5xx responses  

---

# Notes

- Data validation rules depend on datasource configuration  
- Large payloads may be subject to size limits  
- Ingestion behavior may evolve in future API versions  
- Assistant reasoning quality depends heavily on schema consistency  
