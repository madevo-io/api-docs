# Madevo Assistant REST API

## Introduction

The Madevo Assistant REST API provides programmatic access to the Madevo AI assistant platform. It enables developers and partners to authenticate users, interact with AI assistants through conversational sessions, and ingest structured data into Madevo data sources for analysis, automation, and reporting.

The API is designed around REST principles and uses JSON for all request and response payloads.

## Base URL

Development environment  
https://dev.madevo.ai/api/v1

Production environment  
https://app.madevo.ai/api/v1

All endpoint paths described in this documentation should be appended to the selected base URL.

## Authentication Overview

The Madevo Assistant API uses token based authentication. Clients must authenticate using an email address and password to obtain an access token. This token must be included in the Authorization header for all protected endpoints.

Authentication flow:

1. Authenticate with email and password to obtain an access token  
2. Include the token in the Authorization header for API requests  
3. Refresh the token when it expires to maintain access  

## Core Capabilities

The API provides the following main capabilities:

- Secure user authentication and token refresh
- Conversational interaction with AI assistants
- Persistent, context aware conversations
- Structured data ingestion into Madevo data sources
- Support for visual and structured assistant outputs

## API Conventions

### Request Format

- All requests must use HTTPS
- Request and response bodies are formatted as JSON
- Content-Type should be set to application/json

### Authorization Header

All protected endpoints require the following header:

Authorization: Bearer YOUR_ACCESS_TOKEN

powershell
Copy code

### Timestamps

Where applicable, timestamps should be provided in ISO 8601 format using UTC.

Example:

2025-01-01T12:00:00Z

csharp
Copy code

## Environments

| Environment | Base URL |
|------------|----------|
| Development | https://dev.madevo.ai/api/v1 |
| Production | https://app.madevo.ai/api/v1 |

## Versioning

The current version of the API is v1. Backwards incompatible changes will be introduced in future versions and documented accordingly.

Clients are encouraged to pin integrations to a specific API version.

## Getting Started

To get started with the Madevo Assistant API:

1. Obtain valid login credentials
2. Authenticate using the login endpoint to receive an access token
3. Use the assistant chat endpoint to interact with an AI assistant
4. Push structured data to a data source if required

Detailed examples for each endpoint are provided in the following sections of this documentation.

## Support

If you encounter issues or have questions about the API, please contact the Madevo team or your designated technical contact.
