# Create Pull Request

**Use the GitHub tool to create a pull request:**

1. Create a PR that links to the JIRA task issue in the description
2. Include the confluence doc link in the description
3. Include a clear summary of what changes were made
4. Add added/changed files with a description
5. Include the context of this PR

**Structure your PR description like this:**

```markdown
Jira Link: {jira_url}
Doc: {confluence_doc_url}

## Summary

{description}

## Changes

New files:

- {file 1} - {change description}
- {file 2} - {change description}

Modified:

- {file 1} - {change description}
- {file 2} - {change description}

## Context

{context}

## Test plan

- {test step 1}
- {test step 2}
```
