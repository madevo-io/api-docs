# Assistant Interaction

The Assistant Interaction API allows clients to communicate with a Madevo AI assistant using natural language. Messages are exchanged within a conversation context, enabling the assistant to maintain memory, understand intent, and provide context aware responses.

---

## Send Message to Assistant

Send a user message to the AI assistant and receive a generated response.

### Endpoint

POST /restapi/assistant/chat

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
  "conversation_id": "12345",
  "message": "Hello, assistant!",
  "skip_history": false,
  "skip_save_history": false
}
```

---

## Request Parameters

| Field | Type | Required | Description |
|------|------|----------|-------------|
| conversation_id | string | Yes | Unique identifier for the conversation |
| message | string | Yes | User message sent to the assistant |
| skip_history | boolean | No | Ignore previous conversation history |
| skip_save_history | boolean | No | Do not store the message and response |

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
|------|------|-------------|
| message | string | Assistant generated response |
| visualization | object | Optional structured output for UI rendering |

---

## Conversation Management

### Conversation ID

The conversation_id groups messages into a single conversational session. Reusing the same conversation_id allows the assistant to maintain context across multiple interactions.

Typical use cases include:

- Follow up questions
- Clarifications
- Multi step reasoning
- Progressive exploration of data

Providing a new conversation_id starts a new conversation.

---

## History Controls

### skip_history

When set to true, the assistant ignores all previous messages in the conversation and responds only to the current message.

This is useful for:

- Stateless queries
- One off questions
- Debugging

### skip_save_history

When set to true, the current message and response are not persisted.

This is useful for:

- Sensitive requests
- Temporary or exploratory queries
- Privacy focused workflows

---

## Example Request

```json
{
  "conversation_id": "network-ops-001",
  "message": "What was the average temperature yesterday?",
  "skip_history": false,
  "skip_save_history": false
}
```

---

## Example Response

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

- Reuse conversation_id for follow up interactions
- Be clear and specific in user messages
- Store access tokens securely
- Refresh tokens before expiration

---

## Notes

- Assistant behaviour may vary based on connected data sources and permissions
- Visualization formats may evolve over time
- Responses are generated dynamically and may differ for similar prompts
****
