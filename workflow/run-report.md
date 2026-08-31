# Weekly report workflow

Use this workflow when asked to run the weekly report.

## Goal
Summarize notable repository activity from the last 7 days.

## Steps
1. List recent workflow runs with `mcp__github_ci__get_ci_status` or `mcp__github_ci__get_workflow_run_details`.
2. Focus on failed runs first and include the likely root cause.
3. Include successful runs only when they are relevant trends.
4. Post a concise summary with:
   - run link
   - status
   - root cause (for failures)
   - suggested next action

## If data is unavailable
If a required run or log cannot be accessed, report that in the output and continue with what is available.
