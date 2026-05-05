---
description: "Workspace instructions for NETOPS project. Defines agent behavior, interaction conventions, and development guidelines for Claude assistant."
---

# NETOPS Workspace Agent Instructions

This workspace uses structured agent rules and tags to control how Claude assists with code and tasks.

## Quick Reference: Agent Tags

| Tag | Meaning | Usage |
|-----|---------|-------|
| `[[ans]]` | Answer only, no code modification | Use when you want explanation without changes |
| `[[arch]]` | Write architecture documentation markdown | Use when you need system architecture documented |
| `[[brief]]` | Quick answer mode, no deep analysis | Use when you need fast answers without extensive research |
| `[[sw]]` | Software design pattern compliance | Use when you want code to follow established patterns |
| `[[min]]` | Minimum feasible implementation | Use when you want only core functionality, no extra features |
| `[[doc]]` | Write documentation for repo/module/file | Use when you need clear, structured documentation |

**Example:**
```
[[ans]] What does the probe_loop module handle?
```
→ Response: Explanation and analysis, no file modifications.

---

## Core Rules

1. **Use [[ans]] when you need explanation** - Add this tag to get focused answers without code changes
2. **Direct implementation otherwise** - The agent will modify code and create files as needed
3. **Task tracking** - Complex work uses todo lists for progress visibility
4. **Context-driven** - Tools are used to understand code before making changes

---

## Project Structure

```
NETOPS/
├── app/              # Main application code
│   ├── api/          # REST API endpoints
│   ├── actions/      # System actions (DNS, routes, etc)
│   ├── core/         # Core functionality
│   └── services/     # Business logic services
├── deployment/       # Infrastructure configs
├── docs/             # Operational documentation
├── DESIGN/           # System specifications (SPEC-v*.md)
└── tests/            # Test suite
```

---

## Common Tasks

### Get Help Understanding Code
```
[[ans]] How does the reconciliation loop work?
```

### Get Quick Answers
```
[[brief]] What modules are in the api directory?
```

### Document Architecture
```
[[arch]] Create architecture documentation for the decision service
```

### Implement a Feature
```
Add support for new device type with parameters X, Y, Z
```

### Implement Following Design Patterns
```
[[sw]] Add a new service handler following the established patterns
```

### MVP Development
```
[[min]] Add basic health check endpoint
```

### Write Documentation
```
[[doc]] Write a comprehensive guide for the authentication system
[[doc]] Document the config.py module with examples
```

### Debug an Issue
```
[[ans]] Why is metric collection failing?
Then fix it.
```

### Review & Refactor
```
[[ans]] What performance issues do you see in storage_handler.py?
Then optimize it.
```

---

## Development Standards

- **Python Version:** 3.11+ (see pyproject.toml)
- **Linting:** Use ruff (configured in ruff.toml)
- **Testing:** Place tests in tests/ directory
- **Documentation:** Update docs/ for operational changes

---

## Related Guidance

See [Claude Agent Rules](./instructions/claude-agent-rules.instructions.md) for comprehensive agent behavior guidelines, interaction patterns, and tool usage conventions.
