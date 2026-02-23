# Data Schema and Semantics

## Purpose

This guide defines the required structure, formatting standards, and naming conventions for data ingested into Madevo datasources.

Following these standards ensures:

- Accurate Assistant responses  
- Reliable Agent execution  
- Correct time-based filtering  
- Deterministic query generation  
- Reduced ingestion errors  

Schema inconsistency is the most common cause of incorrect AI output.

---

## Core Data Principles

All datasources should follow these principles:

1. Structured, tabular format  
2. One logical record per row  
3. Explicit timestamp per record  
4. Stable column names  
5. Consistent data types per column  

Madevo operates on structured reasoning. Ambiguous or inconsistent schemas reduce reliability.

---

## Timestamp Requirements (Mandatory)

Every record must include a timestamp field.

### Requirements

- ISO 8601 format  
- Must include timezone information  
- Preferably stored in UTC  

### Accepted Examples

```text
2024-01-01T10:00:00Z
2024-01-01T10:00:00+00:00
2024-01-01T12:30:15+01:00
```

### Not Accepted

```text
01/01/2024 10:00
2024-01-01 10:00
2024-01-01T10:00:00
```

Missing or incorrectly formatted timestamps can cause:

- Empty query results  
- Incorrect time filtering  
- Assistant returning no data  

---

## Recommended Record Structures

Madevo supports both narrow and wide formats. Choose one format per datasource and remain consistent.

### Narrow Format

```json
{
  "timestamp": "2024-01-01T10:00:00Z",
  "entity_id": "S005",
  "metric_name": "packet_loss_pct",
  "value": 0.8
}
```

### Wide Format

```json
{
  "timestamp": "2024-01-01T10:00:00Z",
  "sensor_id": "S005",
  "packet_loss_pct": 0.8,
  "latency_ms": 12,
  "traffic_in_bps": 5023000
}
```

Both are supported. Avoid mixing structural styles within the same datasource.

---

## Naming Conventions

To ensure predictable query generation:

- Use snake_case for column names  
- Avoid spaces in column names  
- Avoid special characters  
- Do not dynamically rename metrics between uploads  

### Good Examples

```text
packet_loss_pct
latency_ms
traffic_in_bps
temperature_c
home_score
```

### Avoid

```text
Packet Loss %
Latency (ms)
Traffic-In-Bps
Metric1
Value2
```

Consistent naming directly improves assistant accuracy.

---

## Data Type Consistency

Each column must maintain a consistent type:

- Numeric metrics must remain numeric  
- Identifiers should remain strings  
- Status fields should use consistent enumerated values  

Do not mix types in the same column:

```text
12
"12"
"twelve"
```

Mixed types may result in:

- Query failures  
- Incorrect aggregations  
- Agent instability  

---

## Time-Series Design Rules

For reliable time-based reasoning:

- One row equals one timestamped observation  
- Do not embed arrays inside a single record  
- Do not store historical ranges inside one field  
- Avoid multiple timestamps per row  

### Correct

| timestamp | sensor_id | latency_ms |
|-----------|-----------|------------|
| 10:00     | S005      | 12         |
| 10:01     | S005      | 15         |

### Incorrect

| sensor_id | last_24h_latency |
|-----------|------------------|
| S005      | [12,15,14,13...] |

Madevo expects explicit time records for temporal analysis.

---

## Schema Stability

Avoid changing:

- Column names  
- Timestamp format  
- Data types  

If a schema change is required:

1. Create a test datasource.  
2. Validate Assistant queries.  
3. Confirm Agent compatibility.  
4. Deploy to production only after verification.  

Uncontrolled schema changes are a common cause of production instability.

---

## Large Dataset Guidelines

For large-scale ingestion:

- Maintain consistent ingestion frequency  
- Avoid irregular timestamp gaps where possible  
- Ensure timestamp reflects event time, not ingestion time  
- Avoid duplicate records  

If using streaming ingestion, ensure chronological ordering where feasible.

---

## Validation Checklist

Before uploading or updating a datasource, confirm:

- Timestamps are ISO 8601 with timezone  
- Column names use snake_case  
- No nested structures in CSV fields  
- Data types are consistent per column  
- Each row represents one logical record  
- Schema matches previous uploads  

---

## Summary

Clean, stable, and well-structured data leads directly to:

- More accurate Assistant responses  
- More reliable Agent execution  
- Predictable analytical results  

When in doubt, simplify the schema and validate using datasource preview before querying.
