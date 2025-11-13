---
name: ai-commit
description: Create intelligent commit messages for git changes. Use this skill when the user wants to create a commit, stage changes and commit, or asks for help with commit messages. Analyzes staged or unstaged changes and generates appropriate commit messages based on user preferences (conventional commits, custom formats, etc.).
---

# AI Commit

## Overview

Generate intelligent, context-aware commit messages based on code changes. The skill adapts to user preferences for commit message formats (conventional commits, custom formats) and can optionally push changes after committing.

## First-Time Setup

On first use, check if preferences file exists at `preferences.md` in this skill directory. If not, ask the user these setup questions:

1. **Commit Message Format**: "What commit message format do you prefer?"
   - Conventional Commits (e.g., `feat: add login functionality`)
   - Custom format (ask for details and examples)
   - Simple descriptive (e.g., `Add login functionality`)

2. **Auto-Push Behavior**: "Should commits be automatically pushed to the remote repository?"
   - Yes - always push after committing
   - No - only commit locally
   - Ask each time

3. **Agent Attribution**: "Should the AI agent be mentioned in commit messages?"
   - Yes - include agent attribution in commit footer
   - No - omit agent attribution

After collecting answers, write the preferences to `preferences.md` in this skill directory using this format:

```
format: conventional
auto_push: yes
mention_agent: yes
```

or

```
format: simple
auto_push: no
mention_agent: no
```

or

```
format: custom
custom_template: {type}: {description}
auto_push: ask
mention_agent: yes
```

Load existing preferences at the start of each commit workflow by reading the `preferences.md` file.

## Commit Workflow

### Step 1: Check Git Status

Run `git status` to determine:

- Which files are staged
- Which files are unstaged
- Current branch information

### Step 2: Determine Scope

**If files are staged**: Only analyze staged changes for the commit message
**If no files are staged**: Stage all changes (`git add .`) and analyze all changes

### Step 3: Analyze Changes

Run `git diff --staged` (or `git diff` if staging all) to understand:

- What code was added, modified, or deleted
- Which files and functions were affected
- The nature of the changes (feature, fix, refactor, docs, etc.)

Also run `git log --oneline -10` to understand the repository's commit message style and conventions.

### Step 4: Generate Commit Message

Based on user preferences and change analysis, craft an appropriate commit message:

**For Conventional Commits format**:

```
<type>(<scope>): <description>

<optional body>
```

Types: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`, `perf`, `ci`, `build`, `revert`

Example:

```
feat(auth): add user login functionality

Implement JWT-based authentication with secure token storage
and automatic session refresh
```

**For Simple Descriptive format**:

```
<Clear description of what changed>

<Optional details about why or how>
```

Example:

```
Add user login functionality

Implement authentication system with JWT tokens
```

**For Custom formats**: Follow the user's specified format pattern

### Step 5: Create Commit

Execute the commit with the generated message. If `mention_agent` preference is "yes", append attribution footer:

```bash
git commit -m "$(cat <<'EOF'
<commit message>

🤖 Generated with [Claude Code](https://claude.com/claude-code)

Co-Authored-By: Claude <noreply@anthropic.com>
EOF
)"
```

If `mention_agent` is "no", commit without attribution:

```bash
git commit -m "<commit message>"
```

Note: Adjust the agent name/URL in the attribution based on which AI agent is executing the skill.

### Step 6: Handle Auto-Push

Based on user preferences:

- **If auto-push is "yes"**: Run `git push`
- **If auto-push is "ask"**: Ask the user if they want to push
- **If auto-push is "no"**: Skip pushing

## Commit Message Best Practices

- **Be specific**: Describe what changed, not how
- **Use imperative mood**: "Add feature" not "Added feature"
- **Keep first line concise**: 50-72 characters for the subject
- **Provide context**: Explain why the change was made if not obvious
- **Reference issues**: Include ticket numbers if applicable (e.g., `fixes #123`)
- **Avoid generic messages**: Never use "Update", "Fix", "Changes" alone

## Quick Reference

### Conventional Commit Types
- `feat`: New feature | `fix`: Bug fix | `docs`: Documentation | `style`: Formatting
- `refactor`: Code restructure | `perf`: Performance | `test`: Tests | `chore`: Maintenance

### Good Commit Patterns
- Features: "Add [feature]", "Implement [functionality]"
- Fixes: "Fix [specific problem]", "Resolve [issue]"
- Refactors: "Extract [code] into [destination]", "Simplify [area]"

### What Makes a Good Commit
- ✅ Specific and clear ("Fix null check in payment processing")
- ✅ Imperative mood ("Add feature" not "Added feature")
- ✅ Explains why, not how
- ❌ Vague ("Update files", "Fix bug")
- ❌ Multiple unrelated changes in one commit

## Common Scenarios

### Scenario 1: User wants to commit all changes

```
User: "Commit my changes"
→ Check if files are staged
→ If not, stage all files with git add .
→ Analyze all changes
→ Generate commit message based on preferences
→ Commit and handle auto-push
```

### Scenario 2: User has specific files staged

```
User: "Make a commit"
→ Detect staged files exist
→ Only analyze staged changes
→ Generate focused commit message
→ Commit staged files only
→ Handle auto-push
```

### Scenario 3: First-time user

```
User: "Help me commit this"
→ No preferences file found
→ Run first-time setup
→ Save preferences
→ Proceed with commit workflow
```
