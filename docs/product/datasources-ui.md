# Datasource (UI)

## Purpose

Create and manage datasources so the Assistant and Agent can access your structured business data.

A correctly configured datasource is required for accurate AI responses and reliable task execution.

---

## Create a Datasource

1. In the left sidebar, click **Datasources**.
2. Click **New Datasource**.
3. Enter a clear, descriptive name.
4. Upload your data file (for example CSV).
5. Click **Save**.
6. Wait for processing to complete.
7. Click **Refresh** if the new datasource does not immediately appear.

![Datasource list page with “New Datasource” button](../screenshots/datasource-list.png)

![Datasource creation modal with upload section visible](../screenshots/datasource-create.png)

---

## Expected Result

After successful creation:

- The datasource appears in the list.
- Metadata is visible:
  - File count
  - Record count
  - Last updated timestamp
- Status indicates processing is complete.

---

## Preview and Validate Data

Before using the datasource in Assistant or Agent:

1. Locate the datasource in the list.
2. Click **View**.
3. Confirm:
   - Timestamp column exists.
   - Column names match expectations.
   - Data values look correct.

![Datasource preview table view showing timestamp column](../screenshots/datasource-preview.png)

Validating data immediately after upload prevents incorrect AI responses later.

---

## Schema Requirements (Important)

For reliable operation:

- Timestamps must use ISO 8601 format.
- Timestamps must include timezone information.
- Each row must represent one logical record.
- Column names must remain consistent across uploads.
- Avoid nested JSON structures when uploading CSV files.

For full standards, see:
[Data Schema and Semantics](data-schema.md)

---

## Common Issues

### Upload Fails
- Verify file type and size.
- Confirm file encoding (UTF-8 recommended).

### Datasource Not Visible
- Click **Refresh**.
- Confirm processing completed successfully.

### Stuck in Processing
- Wait briefly.
- Refresh the page.
- If persistent, re-upload the file.

### Incorrect Records in Preview
- Check timestamp formatting.
- Verify column naming consistency.
- Re-upload corrected data if needed.

---

## Best Practices

- Use stable naming conventions (snake_case).
- Keep metric names consistent across updates.
- Avoid frequent schema changes.
- Validate in preview before using in Assistant or Agent.
- Maintain consistent ingestion intervals.

A clean and stable datasource directly improves Assistant accuracy and Agent reliability.
