# Task 2 – GitHub Top Repository Monitor

## Overview

This workflow runs on a schedule and monitors GitHub repositories related to Python. It retrieves repository data from the GitHub public API, selects the top 5 repositories based on star count, enriches the results using a second GitHub API request, and sends the final summary to Telegram.

## Workflow

Schedule Trigger
→ GitHub Repository Search API
→ JavaScript Transformation
→ GitHub README API
→ JavaScript Enrichment
→ IF (stars > 10,000)
→ Telegram Notification

An additional error branch handles failures from the GitHub API and sends an error notification through Telegram.

## APIs Used

1. GitHub Search API
   - Searches public GitHub repositories using the query `language:python`.
   - Results are sorted by stars in descending order.

2. GitHub Repository Contents API
   - Fetches README information for each selected repository.

## Transformation

The workflow extracts the top 5 repositories and keeps relevant fields such as:

- Repository name
- Full repository name
- Owner
- Star count
- Description
- GitHub URL

The second API call enriches each repository with README information.

## Conditional Logic

The IF node checks:

`stars > 10000`

Repositories meeting the threshold continue to the Telegram notification branch.

## Notification

Telegram is used for notifications. The workflow sends the top 5 repository summary including repository names, star counts and GitHub URLs.

Telegram credentials are stored in n8n Credentials rather than hard-coded in the workflow.

## Error Handling

The GitHub API request has a separate error path. If the API request fails, the workflow sends an error notification to Telegram instead of silently failing.

## Testing

The workflow was manually executed and verified successfully.

Tested:

- GitHub API request
- Top 5 repository transformation
- README enrichment
- Star-count IF condition
- Telegram success notification
- GitHub API error notification
