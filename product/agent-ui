# Agent (UI)

## Purpose

Agents allow you to create repeatable, structured AI tasks that run against selected datasources.

Unlike the Assistant, which is conversational and interactive, Agents are designed for controlled, task-based execution and operational workflows.

---

## Create a New Agent Task

1. In the left sidebar, click **Agent**.
2. Click **New Task**.
3. Enter a task name in **Name your task...**.
4. Enter detailed instructions in **Describe your task...**.
5. Open **Select Data Source** and choose one or more datasources.
6. Click **Add** to create the task.

![Agent task list page with New Task button](../screenshots/agent-list.png)

![Agent creation dialog with name, instructions, and datasource selector](../screenshots/agent-create.png)

---

## Run a Task

1. Locate the task in the task list.
2. Click **Run**.
3. Monitor execution status until completion.

![Agent execution status view showing running or completed state](../screenshots/agent-status.png)

Possible execution states include:

- Pending  
- Running  
- Completed  
- Failed  

---

## Writing Effective Agent Instructions

Agent reliability depends on instruction clarity.

For best results:

- Define a specific time range.
- Use exact metric names.
- Reference specific identifiers.
- State expected output format if necessary.

### Example Instruction

Analyze traffic_in_bps over the last 24 hours and identify anomalies greater than 20 percent deviation from the rolling average.

Avoid vague instructions such as:
Analyze performance trends.

---

## Reviewing Results

After execution:

- Confirm the correct time range was applied.
- Validate that referenced metrics exist in the datasource.
- Check logical consistency of output.
- Refine instructions if needed.

Unexpected output is commonly caused by:

- Ambiguous instructions  
- Schema inconsistencies  
- Timestamp formatting issues  

---

## Common Issues

### Task Not Created
- Ensure both task name and instructions are entered.
- Confirm at least one datasource is selected.

### Datasource Dropdown Empty
- Create and process a datasource first.

### Task Fails During Execution
- Review instruction clarity.
- Validate datasource schema.
- Confirm data exists for the requested time range.

### Output Is Incorrect
- Narrow the scope of the task.
- Reference explicit metric names.
- Add a defined time constraint.

---

## Best Practices

- Keep task instructions structured and specific.
- Avoid frequent schema changes in datasources.
- Test new tasks manually before relying on them operationally.
- Monitor early executions after major updates.

Well-defined instructions combined with clean data structure result in stable and reliable agent execution.
