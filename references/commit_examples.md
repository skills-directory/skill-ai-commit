# Commit Message Examples

## Good Examples

### Example 1: Clear Feature Addition

```
Add user profile settings page

Create new settings interface allowing users to update
their display name, email, and notification preferences.
Includes form validation and error handling.
```

**Why it's good:**

- Clear subject line describing what was added
- Explains what the feature does
- Mentions important implementation details

### Example 2: Specific Bug Fix

```
Fix memory leak in websocket connection handler

Properly close and clean up websocket connections when
component unmounts to prevent memory accumulation during
navigation between pages.

Fixes #456
```

**Why it's good:**

- Identifies the specific problem
- Explains the solution
- References the issue number

### Example 3: Refactoring with Context

```
Extract authentication logic into reusable hook

Move JWT token management and refresh logic from individual
components into a shared useAuth hook. This reduces code
duplication and makes authentication behavior consistent
across the application.
```

**Why it's good:**

- Describes what changed
- Explains why the change was made
- Clarifies the benefit

### Example 4: Documentation Update

```
Update API documentation for user endpoints

Add missing query parameters for /users endpoint and
correct response schema examples to match current API
implementation.
```

**Why it's good:**

- Specific about what documentation changed
- Mentions what was added/corrected

## Bad Examples (and How to Improve)

### Example 1: Too Vague

```
❌ BAD: Update files

✅ GOOD: Refactor user authentication to use JWT tokens

Replace session-based authentication with JWT tokens
for improved scalability and stateless API design.
```

**Problem:** "Update files" doesn't explain what changed or why

### Example 2: Missing Context

```
❌ BAD: Fix bug

✅ GOOD: Fix null pointer exception in payment processing

Add null check before accessing payment gateway response
to handle cases where the gateway times out.

Fixes #789
```

**Problem:** Doesn't specify which bug or where it occurred

### Example 3: Too Technical (How instead of What/Why)

```
❌ BAD: Change useState to useReducer in UserContext.tsx

✅ GOOD: Improve state management in user context

Replace useState with useReducer to better handle complex
state updates and make state transitions more predictable.
```

**Problem:** Focuses on implementation details instead of the purpose

### Example 4: Multiple Unrelated Changes

```
❌ BAD: Fix login bug, update README, refactor utils

✅ GOOD: Split into separate commits:
  1. Fix login validation error handling
  2. Update README with setup instructions
  3. Extract date formatting utilities
```

**Problem:** Commits should focus on a single logical change

### Example 5: WIP or Placeholder Messages

```
❌ BAD: WIP
❌ BAD: temp commit
❌ BAD: asdf
❌ BAD: fixes

✅ GOOD: Always write descriptive messages, even for work in progress
```

**Problem:** These provide no information and clutter history

## Commit Message Patterns by Change Type

### New Features

```
Add [feature name]
Implement [functionality]
Create [new component/module]
```

Example: `Add dark mode toggle to user preferences`

### Bug Fixes

```
Fix [specific problem]
Resolve [issue description]
Correct [incorrect behavior]
```

Example: `Fix incorrect total calculation in shopping cart`

### Refactoring

```
Refactor [component/module] to [improvement]
Extract [code] into [destination]
Simplify [complex code area]
```

Example: `Refactor data fetching to use React Query`

### Performance

```
Optimize [slow operation]
Improve performance of [feature]
Reduce [resource usage] in [area]
```

Example: `Optimize image loading with lazy loading`

### Tests

```
Add tests for [feature/component]
Update tests to cover [scenario]
Fix failing test in [test suite]
```

Example: `Add unit tests for authentication hooks`

### Documentation

```
Update [doc type] for [feature]
Add documentation for [new feature]
Clarify [confusing section] in [doc]
```

Example: `Update API documentation for search endpoints`

### Dependencies

```
Upgrade [package] to [version]
Add [package] for [purpose]
Remove unused [package]
```

Example: `Upgrade React to v18 for concurrent features`

## Multi-Line Commit Guidelines

When changes require more explanation, use a multi-line format:

```
<summary line (50-72 chars)>

<blank line>

<detailed description wrapped at 72 characters explaining
what changed and why. Use multiple paragraphs if needed.>

<blank line>

<optional footer with issue references>
```

Example:

```
Implement OAuth2 authentication flow

Replace custom authentication with OAuth2 to improve
security and enable integration with third-party identity
providers. The implementation includes:

- Authorization code flow with PKCE
- Automatic token refresh
- Secure token storage in httpOnly cookies
- Integration with existing user management system

This change requires users to re-authenticate on next
login but provides better security and paves the way for
social login features.

Closes #123, Relates to #456
```

## Tips for Writing Great Commit Messages

1. **Write in imperative mood**: "Add feature" not "Added feature" or "Adds feature"
2. **Be specific**: "Fix login error on mobile Safari" beats "Fix login"
3. **Explain why, not how**: Code shows how, commit message explains why
4. **Keep subject line short**: Aim for 50-72 characters
5. **Use body for complexity**: If change needs explanation, add details in body
6. **Reference issues**: Link to bug reports or feature requests
7. **Think about reviewers**: What would you want to know reviewing this change?
8. **Commit atomically**: One logical change per commit
