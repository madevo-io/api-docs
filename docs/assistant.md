
# Assistant Interaction

The Assistant Interaction API allows clients to communicate with a Madevo AI assistant using natural language. Messages are sent within a conversation context, enabling the assistant to maintain memory, understand intent, and provide context aware responses.

This endpoint supports both simple conversational queries and advanced, data driven interactions.

---

## Send Message to Assistant

Sends a user message to the AI assistant and returns the assistant generated response.

### Endpoint

POST /restapi/assistant/chat

---

## Authentication

This endpoint requires authentication.

### Required Headers

Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

yaml
Copy code

---

## Request Body

```json
{
  "conversation_id": "12345",
  "message": "Hello, assistant!",
  "skip_history": false,
  "skip_save_history": false
}
Request Parameters
Field	Type	Required	Description
conversation_id	string	Yes	Unique identifier for the conversation session
message	string	Yes	User message sent to the assistant
skip_history	boolean	No	If true, previous conversation history is ignored
skip_save_history	boolean	No	If true, the message and response are not persisted

Response
json
Copy code
{
  "message": "Hello! How can I assist you today?",
  "visualization": {}
}
Response Fields
Field	Type	Description
message	string	Assistant generated natural language response
visualization	object	Optional structured output for UI components

The visualization field may contain structured data intended for charts, tables, or other frontend visual elements. If no visualization is applicable, this field may be empty.

Conversation Management
Conversation ID
The conversation_id groups messages into a single conversational session. Reusing the same conversation_id allows the assistant to maintain context across multiple requests.

Examples of context aware interactions include:

Follow up questions

Clarifications

Multi step reasoning

Progressive data exploration

If a new conversation_id is provided, the assistant will start a new conversation context.

History Controls
skip_history
When set to true, the assistant will ignore any previous messages associated with the conversation_id and respond only to the current message.

This is useful for:

Stateless queries

One off questions

Debugging responses

skip_save_history
When set to true, the current message and assistant response will not be stored. Future messages using the same conversation_id will not include this interaction.

This is useful for:

Sensitive queries

Temporary or exploratory prompts

Privacy sensitive workflows

Example Request
json
Copy code
{
  "conversation_id": "network-ops-001",
  "message": "What was the average temperature yesterday?",
  "skip_history": false,
  "skip_save_history": false
}
Example Response
json
Copy code
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
Error Responses
Status Code	Meaning
400	Invalid request payload
401	Unauthorized or missing token
403	Access forbidden
500	Internal server error

Error responses may include a descriptive message to assist with troubleshooting.

Best Practices
Reuse conversation_id for follow up questions

Use clear and specific messages for better responses

Store access tokens securely

Refresh tokens before expiration

Avoid sharing sensitive information unless required

