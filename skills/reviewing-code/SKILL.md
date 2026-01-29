---
name: reviewing-code
description: Reviews code changes for bugs, performance issues, security problems, and best practice violations. Use when reviewing PRs, before committing, after making code changes, or when user asks to review, check, or look over code. Catches N+1 queries, missing error handling, React hooks issues, test coverage gaps, and security vulnerabilities.
---

# Reviewing Code

## Overview

Review code changes systematically using priority-based rules. Focus on what automated linters miss — performance, architecture, test coverage, and security patterns.

## Review Workflow

1. **Identify changed files** — focus review on actual changes, not entire codebase
2. **Check P0 rules first** — blocking issues stop the review
3. **Check P1 rules** — important issues that need discussion
4. **Optionally check P2** — only if user wants a thorough review
5. **Provide fixes** — include code suggestions for each issue

## Priority Levels

- **P0: Blocking** — must fix before merge
- **P1: Important** — should fix, discuss if not
- **P2: Nice-to-have** — suggest but don't block

## What to Check

### P0 — Blocking Issues

| Category | What to look for |
|----------|-----------------|
| **N+1 queries** | Database/API call inside a loop; resolver without batching |
| **Security** | Missing auth check on endpoint; fail-open permission pattern; SQL injection; XSS |
| **Data loss** | Missing error handling on write operations; no transaction for multi-step mutations |
| **Memory leaks** | Uncleaned subscriptions, timers, or event listeners in effects |

### P1 — Important Issues

| Category | What to look for |
|----------|-----------------|
| **Performance** | O(n²) when O(n) is possible; expensive computation in render path; missing memoization for derived data; large bundle imports |
| **Error handling** | Missing try/catch on async operations; swallowed errors; missing error boundaries |
| **Test coverage** | New business logic without tests; untested error paths; missing edge cases |
| **Null safety** | Accessing nested properties without null checks; missing optional chaining |
| **React hooks** | Missing dependencies in useEffect; missing cleanup functions; hooks inside conditions |

### P2 — Nice to Have

| Category | What to look for |
|----------|-----------------|
| **Naming** | Unclear variable/function names; inconsistent naming patterns |
| **Code organization** | Logic in wrong layer (UI doing business logic); duplicated code |
| **Types** | Missing type annotations on public APIs; `any` types |
| **Clean code** | Magic numbers; deeply nested conditionals; functions doing too many things |

## Human Blind Spots — Prioritize These

These are rarely caught by human reviewers. The skill must catch them:

1. **Performance** — O(n) vs O(1) lookups, unnecessary re-renders, bundle size impact
2. **Test coverage** — missing tests for new logic, untested error paths
3. **Memory leaks** — uncleaned subscriptions, timers, event listeners

## Explanation Style

**DO:** Provide full verbal explanations
```
"This calls the user service inside a loop. With 50 users, that's
51 database calls instead of 2. Batch the IDs and make a single
query with a WHERE IN clause."
```

**DON'T:** Leave terse comments without context
```
"N+1 query"
```

## Output Format

For each issue:

```markdown
### [P0] Short Description

**File:** path/to/file.ts:42

**Issue:** [Full explanation of the problem and its impact]

**Fix:**
// Before
[problematic code]

// After
[fixed code]
```

## Inline Code Markers

When reviewing code in-place, use these markers:

```
// FIXME(review): [P0] N+1 query — will cause performance degradation at scale
// TODO(review): [P1] Add error handling for network failure case
// NIT(review): Consider renaming for clarity
```

## After Review

Present the summary with issue counts by severity, then ask the user what to do next:
- Post comments to GitHub PR
- Create tasks to track fixes
- Just show the summary

## Red Flags — STOP and Review

| Thought | Reality |
|---------|---------|
| "This is too simple to review" | Simple changes break things. Review. |
| "Tests pass so it's fine" | Tests can't catch what they don't cover. Review. |
| "It's just a refactor" | Refactors introduce subtle bugs. Review. |
| "The linter will catch it" | Linters miss logic, performance, and architecture. Review. |
