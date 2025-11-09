# Conventional Commits Specification

## Format

```
<type>(<scope>): <description>

[optional body]

[optional footer(s)]
```

## Types

- **feat**: A new feature for the user
- **fix**: A bug fix
- **docs**: Documentation only changes
- **style**: Changes that don't affect code meaning (formatting, missing semicolons, etc.)
- **refactor**: Code change that neither fixes a bug nor adds a feature
- **perf**: Code change that improves performance
- **test**: Adding missing tests or correcting existing tests
- **chore**: Changes to build process or auxiliary tools
- **ci**: Changes to CI configuration files and scripts
- **build**: Changes that affect the build system or external dependencies
- **revert**: Reverts a previous commit

## Scope

The scope is optional and provides additional contextual information:

- **feat(auth)**: Feature related to authentication
- **fix(api)**: Bug fix in the API
- **docs(readme)**: Documentation update to README

## Description

- Use imperative, present tense: "change" not "changed" nor "changes"
- Don't capitalize first letter
- No period (.) at the end
- Keep it concise (50-72 characters)

## Body

- Use the body to explain what and why vs. how
- Wrap at 72 characters
- Separate from subject with a blank line

## Footer

- Reference issues, breaking changes
- BREAKING CHANGE: introduces a breaking API change
- Closes #123, Fixes #456

## Examples

### Simple Feature

```
feat(login): add remember me checkbox

Allow users to stay logged in across sessions by storing
a persistent token in local storage
```

### Bug Fix

```
fix(api): handle null response from user endpoint

Add null check before accessing user data properties to
prevent TypeError when endpoint returns empty response

Fixes #234
```

### Breaking Change

```
feat(api)!: remove deprecated v1 endpoints

BREAKING CHANGE: v1 API endpoints have been removed.
Migrate to v2 endpoints as documented in the migration guide.

Closes #567
```

### Documentation

```
docs(contributing): update code review process

Clarify the expected turnaround time for code reviews
and add guidelines for providing constructive feedback
```

### Refactoring

```
refactor(user-service): simplify authentication logic

Extract JWT validation into separate helper function
to improve code readability and testability
```

## Benefits

1. **Automated Changelogs**: Tools can generate changelogs from commit history
2. **Semantic Versioning**: Automatically determine version bumps
3. **Clear History**: Easy to understand what changed and why
4. **Better Collaboration**: Team members quickly understand commit purpose
5. **Tooling Integration**: Works with release automation tools
