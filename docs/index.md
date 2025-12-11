# Madevo Assistant REST API

## Introduction

The Madevo Assistant REST API provides programmatic access to the Madevo AI assistant platform. It allows clients to authenticate users, interact with AI assistants through conversational sessions, and ingest structured data into Madevo data sources for analysis and automation.

The API follows REST principles and uses JSON for all request and response payloads.

## Base URL

Development environment  
https://dev.madevo.ai/api/v1

Production environment  
https://app.madevo.ai/api/v1

All endpoints documented below should be appended to the selected base URL.

## Authentication Overview

The API uses token based authentication. Clients must first authenticate using an email and password to obtain an access token. This token must be included in the Authorization header for all protected endpoints.

## Main Capabilities

- User authentication and token refresh  
- Conversational interaction with AI assistants  
- Context aware conversations  
- Structured data ingestion into Madevo data sources  
