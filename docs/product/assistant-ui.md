# Assistant (UI)

## Purpose

The Assistant provides conversational access to your datasources.  
It dynamically generates structured queries, retrieves relevant records, and returns contextual responses based on your data.

Assistant accuracy depends heavily on datasource quality and prompt clarity.

---

## Create a Conversation

1. In the left sidebar, click **Assistant**.
2. Click **New**.
3. Enter a conversation name.
4. Click **Save**.
5. Select the newly created conversation from the list.

![Assistant conversation list with New button](../screenshots/assistant-conversation-list.png)

![New conversation modal](../screenshots/assistant-new-conversation.png)

---

## Send a Message

1. Type your question in the message input field.
2. Click **Send**.
3. Wait for the assistant response.

![Assistant chat interface with input field and response visible](../screenshots/assistant-chat.png)

Your message appears in the thread, followed by the assistant’s response.

---

## How the Assistant Uses Your Data

When you send a message:

1. The system analyzes your prompt.
2. Relevant datasources are identified.
3. Structured queries are generated.
4. Records are retrieved.
5. Results are summarized into a natural language response.

If no relevant data is found, the assistant may return an empty or “no data available” response.

---

## Writing Effective Prompts

For reliable results:

- Specify time ranges explicitly.
- Use exact metric names from your datasource.
- Reference identifiers (sensor_id, match_id, device_id, etc.).
- Avoid vague requests.

### Example

Instead of:
Show network issues.

Use:
Show packet_loss_pct for Sensor S005 between 2024-01-01T00:00:00Z and 2024-01-01T23:59:59Z.

Clear prompts improve determinism and accuracy.

---

## Common Issues

### No Data Returned
- Confirm the datasource contains data within the requested time range.
- Verify timestamp format includes timezone.
- Ensure metric names match exactly.

### Low Quality or Unexpected Response
- Narrow the time window.
- Reference explicit field names.
- Avoid combining multiple unrelated questions.

### Assistant Not Responding
- Refresh the page.
- Confirm backend connectivity.
- Wait briefly if ingestion is running.

---

## Best Practices

- Keep datasources structurally consistent.
- Use precise metric naming.
- Validate data in preview before querying.
- Ask one analytical question at a time when debugging.
- Review outputs critically before acting on them.

Reliable datasource structure combined with clear prompts leads to the most accurate Assistant results.
