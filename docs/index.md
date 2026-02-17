# Madevo REST API

## Introduction

The Madevo REST API provides programmatic access to the Madevo AI platform.

It enables developers and partners to:

- Authenticate users securely  
- Interact with AI assistants through conversational sessions  
- Ingest structured data into Madevo datasources  
- Perform operational analysis and automation workflows  

The API follows REST principles and uses JSON for all request and response payloads.

---

## Base URL

All endpoint paths described in this documentation must be appended to the appropriate base URL.

### Development Environment

```
https://dev.madevo.ai/api/v1
```

### Production Environment

```
https://app.madevo.ai/api/v1
```

---

## Core Capabilities

The API provides the following capabilities:

- Secure authentication and token refresh  
- Conversational interaction with AI assistants  
- Persistent, context-aware conversation sessions  
- Structured data ingestion into Madevo datasources  
- Support for Markdown and structured assistant outputs  
- Automation-friendly response patterns  

---

## Authentication Overview

The Madevo API uses token-based authentication.

Authentication flow:

1. Authenticate with email and password to obtain an access token  
2. Include the token in the `Authorization` header for protected endpoints  
3. Refresh the token when it expires  

All protected endpoints require:

```
Authorization: Bearer YOUR_ACCESS_TOKEN
```

See the Authentication section for full details.

---

## API Conventions

### Request Format

- All requests must use HTTPS  
- Request and response bodies are formatted as JSON  
- `Content-Type` must be set to `application/json`  

---

### Timestamps

Where applicable, timestamps must be provided in ISO 8601 format using UTC.

Example:

```
2025-01-01T12:00:00Z
```

---

## Environments

| Environment  | Base URL                          |
|-------------|-----------------------------------|
| Development | https://dev.madevo.ai/api/v1      |
| Production  | https://app.madevo.ai/api/v1      |

---

## Versioning

The current API version is `v1`.

Backwards incompatible changes will be introduced in future versions and documented accordingly.

Clients are encouraged to pin integrations to a specific API version.

---

## Getting Started

To begin integrating with the Madevo API:

1. Obtain valid login credentials  
2. Authenticate to receive an access token  
3. Call the Assistant endpoint to interact with an AI assistant  
4. Optionally push structured data to a datasource  

Detailed examples are provided in the following sections of this documentation.

---

## Documentation Structure

- **Authentication** — Login and token management  
- **Assistant Interaction** — Conversational AI endpoint  
- **Datasource Management** — Structured data ingestion  
- **Errors and Status Codes** — Error handling and retry guidance  

---

## Support

For technical questions or integration support, contact the Madevo team or your designated technical contact.
