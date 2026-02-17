# Assistant Interaction

The Assistant Interaction API enables natural language communication with a Madevo AI assistant.

Messages are exchanged within a conversation context. This allows the assistant to:

- Maintain conversational memory  
- Perform multi step reasoning  
- Analyze connected datasources  
- Generate structured outputs for automation  

---

## Send Message to Assistant

Send a user message to the AI assistant and receive a generated response.

### Endpoint

```
POST /restapi/assistant/chat
```

---

## Authentication

This endpoint requires authentication.

### Headers

```
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

See the Authentication documentation for token lifecycle details.

---

## Request Body

```json
{
  "conversation_id": "12345",
  "message": "Hello, assistant!",
  "skip_history": false,
  "skip_save_history": false
}
```

---

## Request Parameters

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| conversation_id | string | Yes | Unique identifier for the conversation session |
| message | string | Yes | User instruction sent to the assistant |
| skip_history | boolean | No | If true, ignores previous conversation history |
| skip_save_history | boolean | No | If true, does not persist the message and response |

---

## Response

```json
{
  "message": "Hello! How can I assist you today?",
  "visualization": {}
}
```

---

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| message | string | Assistant generated response |
| visualization | object | Optional structured output for UI rendering |

The structure of `visualization` depends on the requested output format and use case.

---

# Conversation Management

## Conversation ID

The `conversation_id` groups messages into a single conversational session.

Reusing the same `conversation_id` allows the assistant to maintain context across interactions.

Typical use cases:

- Follow up questions  
- Clarifications  
- Multi step reasoning  
- Progressive data exploration  

Providing a new `conversation_id` starts a new session.

---

# History Controls

## skip_history

When set to `true`, the assistant ignores all previous messages in the conversation and responds only to the current message.

Useful for:

- Stateless queries  
- Deterministic tasks  
- Debugging  

---

## skip_save_history

When set to `true`, the current message and response are not persisted.

Useful for:

- Sensitive requests  
- Temporary or exploratory workflows  
- Privacy focused operations  

---

# Controlling Output Format

The assistant’s response format depends on the instructions included in the `message`.

For production systems and automation pipelines, explicitly define the expected output structure.

---

## Requesting Markdown Output

If your client renders rich text:

```json
{
  "conversation_id": "ops-report-001",
  "message": "Reply in Markdown with sections: Summary and Actions. Use a table for KPI values.",
  "skip_history": false,
  "skip_save_history": false
}
```

---

## Requesting Strict JSON Output

For automation workflows, request JSON only with an explicit schema:

```json
{
  "conversation_id": "incident-7421",
  "message": "Return ONLY valid minified JSON. Schema: {\"status\":\"string\",\"priority\":\"low|medium|high\",\"actions\":[\"string\"]}. No extra text.",
  "skip_history": true,
  "skip_save_history": true
}
```

### Validation Recommendation

Clients should:

1. Validate JSON structure before execution  
2. Retry once if parsing fails  
3. Escalate to human review if invalid  

---

# Real Time Analysis Pattern

When interacting with live or frequently updated datasources:

- Reuse the same `conversation_id` for progressive reasoning  
- Include timeframe context in the message  
- Avoid vague queries without temporal boundaries  

Example:

```json
{
  "conversation_id": "stadium-das-live-2026-02-17",
  "message": "Analyze abnormal sensor behavior in the last 10 minutes and return top 3 anomalies with probable cause.",
  "skip_history": false,
  "skip_save_history": false
}
```

For deterministic stateless analysis:

```json
{
  "conversation_id": "stateless-analysis-001",
  "message": "Analyze abnormal sensor behavior between 10:00 and 10:10 UTC. Return top 3 anomalies.",
  "skip_history": true,
  "skip_save_history": false
}
```

---

# Retry and Idempotency

If a request fails due to network or timeout issues:

- Retry using the same `conversation_id`  
- Reuse the exact same `message`  
- Do not modify prompt content during retry  

Recommended retry strategy:

- Maximum 3 attempts  
- Exponential backoff  
- Refresh access token on 401 responses  

Reusing the same `conversation_id` preserves reasoning continuity.

---

# Example Request

```json
{
  "conversation_id": "network-ops-001",
  "message": "What was the average temperature yesterday?",
  "skip_history": false,
  "skip_save_history": false
}
```

---

# Example Response

```json
{
  "message": "The average temperature yesterday was 21.4°C.",
  "visualization": {
    "type": "line_chart",
    "data": [
      { "time": "00:00", "value": 20.1 },
      { "time": "06:00", "value": 20.8 },
      { "time": "12:00", "value": 22.3 },
      { "time": "18:00", "value": 22.4 }
    ]
  }
}
```

---

# Error Responses

| Status Code | Meaning |
|-------------|---------|
| 400 | Invalid request payload |
| 401 | Unauthorized or expired token |
| 403 | Forbidden |
| 429 | Rate limit exceeded |
| 500 | Internal server error |

Error responses may include a descriptive message to assist debugging.

---

# Best Practices

- Reuse `conversation_id` for follow up interactions  
- Use explicit output instructions for automation workflows  
- Validate structured responses before execution  
- Store access tokens securely  
- Refresh tokens before expiration  
- Log request and response pairs for observability  

---

# Notes

- Assistant behavior depends on connected datasources and permissions  
- Visualization formats may evolve  
- Responses are generated dynamically and may differ for similar prompts  
- For critical automation workflows, always validate structured outputs before acting on them  
