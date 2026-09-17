---
name: code-reviewer
description: Reviews staged git changes for bugs, security, and performance. Use when the user asks to "review my changes", "check code", or mentions a code review.
license: MIT
metadata:
  version: "1.0.0"
  author: "dev-team"
---

# Code Reviewer Skill

When this skill is actiaakvated, execute a structured code review on the user's codebase using the following workflow.

## 1. Gather Context
* Run `git diff --staged` to see what changes are ready for commit.
* If no changes are staged, run `git diff HEAD~1` to review the last commit, or ask the user which files they want reviewed.

## 2. Review Checklist
Analyze the code specifically for the following three categories:

### 🔒 Security (Critical)
* **Secrets:** Look for hardcoded API keys, passwords, or tokens.
* **Injection:** Check for raw string concatenation in SQL queries or HTML rendering.
* **Data Handling:** Ensure user inputs are validated and sanitized.

### ⚡ Performance & Logic (High)
* **Resource Leaks:** Check for unclosed file handles, database connections, or missing stream closures.
* **Async Code:** Verify that all promises have proper error handling (`.catch()` or `try/catch`).
* **Complexity:** Flag functions that span longer than 50 lines or contain more than 3 nested loops/conditionals.

### 🎨 Style & Readability (Low)
* **Naming:** Ensure variable and function names are descriptive and follow camelCase standard.
* **Dead Code:** Identify unused imports, commented-out code blocks, or unreachable logic.

## 3. Output Format
Group your findings by severity level: **Critical**, **Warning**, or **Suggestion**. For every issue found, format your response exactly like this:

* **[Severity] File Path (Line Number):** 
  * **Issue:** Short description of the problem.
  * **Fix:** Provide a concrete code block demonstrating the recommended correction.

*If no issues are found, congratulate the developer and give them a thumbs up!*
