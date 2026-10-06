# Notes

## Summary of Changes

I identified and fixed two backend issues.

1. The task status filter was not applied correctly because of SQL AND/OR operator precedence in TaskRepository. I added parentheses around the title/description search conditions so that the status condition is applied correctly.

2. Invalid pagination values such as page=0 and page=-1 caused HTTP 500 errors because a negative index was passed to subList(). I added validation for page and pageSize and return HTTP 400 for invalid values.

## What I Chose Not to Change

I did not change the existing pagination behavior because normal page requests returned the expected number of results and continued correctly between pages. I also avoided broader changes where I could not reproduce a clear bug.

## Biggest Remaining Risk

The biggest remaining risk is that there may be other edge cases or performance issues that were not fully investigated within the available time. With more time, I would perform broader API and input validation testing.

## Tools / AI Used

I used VS Code, Git, browser/API requests, and ChatGPT during the investigation. ChatGPT helped me reason about the SQL operator-precedence issue, identify a safe pagination validation approach, and suggest targeted tests. I reviewed the suggestions, made the code changes, and verified the fixes myself.