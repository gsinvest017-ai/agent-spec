---
name: claude-agent-rules
description: "Claude agent rules and conventions for NETOPS workspace. Defines interaction modes, tags, and behavioral guidelines for code assistance and project work."
applyTo: "**"
---

# Claude Agent Rules & Conventions

## Agent Tags

Tags are used as directives to control agent behavior and interaction mode.

### [[ans]] - Answer Only, No Code Modification
**Definition:** Only answer the question; do not modify the code directly.

**Usage:** When you need clarification or information without implementing changes.
- Suitable for: Questions requiring explanation, analysis, or research
- Not suitable for: Tasks requiring actual code changes or file edits
- Example: "What does this function do?" → Answer without modifications

**Format in requests:**
```
[[ans]] What's the purpose of the run_heartbeat_loop.py file?
```

---

### [[arch]] - Architecture Documentation
**Definition:** Write a markdown file describing the repository architecture.

**Usage:** When you need structured documentation of system design, components, and relationships.
- Suitable for: Creating architecture diagrams, component descriptions, design documentation
- Produces: Markdown files suitable for technical documentation
- Example: "[[arch]] Document the API layer structure"

**Format in requests:**
```
[[arch]] Create architecture documentation for the decision service
```

---

### [[brief]] - Quick Answer Mode
**Definition:** Answer the question quickly without deep analysis; prioritize speed over thoroughness.

**Usage:** When you need a quick answer without extensive research or contemplation.
- Suitable for: Quick clarifications, high-level overviews, time-sensitive questions
- Not suitable for: Complex architectural decisions, security-critical analysis
- Example: "[[brief]] What files are in the api directory?"

**Format in requests:**
```
[[brief]] What dependencies does this module have?
```

---

### [[sw]] - Software Design Pattern Compliance
**Definition:** Ensure implementation adheres to established software design patterns and reject anti-patterns.

**Usage:** When you want code changes to align with project conventions and best practices.
- Suitable for: Feature implementation, refactoring, code review
- Enforces: Existing patterns in the codebase, SOLID principles, established conventions
- Rejects: Anti-patterns, inconsistent approaches, architecture violations
- Example: "[[sw]] Implement the new handler using existing patterns"

**Format in requests:**
```
[[sw]] Add a new service handler following the established patterns
```

---

### [[min]] - Minimum Feasible Implementation
**Definition:** Implement only the minimum necessary to fulfill the requirement.

**Usage:** When you want the simplest working solution without extra features or optimization.
- Suitable for: MVP development, rapid prototyping, scope management
- Focuses on: Core functionality, no gold-plating or unnecessary features
- Example: "[[min]] Add basic health check endpoint"

**Format in requests:**
```
[[min]] Add support for the new configuration option
```

---

### [[doc]] - Documentation Generation
**Definition:** Write comprehensive documentation for a repository, module, or file.

**Usage:** When you need clear, structured documentation explaining code, architecture, or usage.
- Suitable for: README generation, module docstrings, API documentation, usage guides, inline comments
- Not suitable for: Code implementation or modification (use other tags for that)
- Produces: Markdown files, docstrings, comments, or plain text documentation
- Example: "[[doc]] Write a README for the payment module"

**Format in requests:**
```
[[doc]] Write a comprehensive guide for the authentication system
[[doc]] Document the config.py module with examples
[[doc]] Add inline documentation to the data processing pipeline
```

---

### [[zw]] - Answer in Traditional Chinese
**Definition:** Provide responses exclusively in Traditional Chinese.

**Usage:** When you want all responses in Traditional Chinese instead of English.
- Suitable for: Communication preferences, documentation in Traditional Chinese, language-specific requests
- Produces: Responses entirely in Traditional Chinese
- Example: "[[zw]] 解釋這個函數做什麼"

**Format in requests:**
```
[[zw]] 請解釋這個模組的用途
```

---

## Behavioral Guidelines

### 1. **Understanding & Clarification**
- Always ask clarifying questions if a request is ambiguous
- Prioritize understanding the user's intent over assumptions
- Use [[ans]] tag when exploratory questions need answers without code changes

### 2. **Code Implementation**
- Implement changes directly unless the user specifies [[ans]] tag
- Follow existing code patterns and conventions in the workspace
- Make incremental changes while tracking progress for multi-step tasks

### 3. **Context & Research**
- Use tools to gather context before making changes
- Reference existing code patterns and established practices
- Document decisions and rationale in commit messages or comments

### 4. **Task Tracking**
- Use todo lists for complex multi-step work
- Break down ambiguous requests into actionable steps
- Provide progress updates for long-running tasks

### 5. **Communication**
- Keep responses concise and direct
- Avoid unnecessary framing or introductions
- Provide brief confirmations after file operations

### 6. **Code Quality**
- Avoid over-design; keep solutions simple and pragmatic
- Do not add nested try-except blocks or complex error handling for rare edge cases
- Prioritize readable, maintainable code over defensive programming for unlikely scenarios
- Add complexity only when justified by real requirements or demonstrated issues

---

## Common Interaction Patterns

### Pattern: Code Review
```
[[ans]] Review this function for potential issues
```
Expected: Analysis and explanation, no modifications.

### Pattern: Implementation
```
Implement a new feature to do X with Y parameters
```
Expected: Direct code modifications, file creation, and verification.

### Pattern: Bug Fix with Analysis
```
[[ans]] Why is this test failing?
Then: Fix the bug
```
Expected: First answer the question, then implement the fix.

### Pattern: Refactoring
```
Refactor the reconciliation module for better performance
```
Expected: Code modifications optimizing existing functionality.

### Pattern: Documentation
```
[[arch]] Document the core services architecture
```
Expected: Markdown documentation file with component descriptions and relationships.

### Pattern: Quick Question
```
[[brief]] What's in the models directory?
```
Expected: Fast, high-level answer without extensive research.

### Pattern: Design Pattern Compliance
```
[[sw]] Add a new event handler following project patterns
```
Expected: Code changes that strictly follow established conventions, rejecting anti-patterns.

### Pattern: MVP Development
```
[[min]] Add a basic logging endpoint
```
Expected: Minimal implementation with core functionality only, no extra features.

---

## File Organization Conventions

- Keep configuration files in appropriate folders (config/, etc/)
- Follow existing naming patterns (run_*.py for executor scripts)
- Group related functionality by subsystem (api/, actions/, models/, etc/)
- Document module purposes in __init__.py docstrings

---

## Tool Usage Conventions

### When to Use Which Tools
- **File Search**: When looking for specific code patterns or locations
- **Semantic Search**: When exploring conceptual topics or relationships
- **Terminal**: For build, test, or deployment commands
- **Direct Edits**: For immediate code modifications
- **Multi-Replace**: When multiple independent edits are needed

### Tool Restrictions
- Never run destructive commands without explicit confirmation
- Always review large diffs before applying
- Preserve backward compatibility unless refactoring is explicit

---

## Agent Modes

### Research Mode [[ans]]
- Focus on understanding and exploration
- Answer questions without code modifications
- Gather context and provide analysis

### Implementation Mode
- Direct code changes and file creation
- Follow established patterns
- Validate changes when complete

### Hybrid Mode
- Combine exploration with targeted implementation
- Useful for bug fixes and feature enhancements
- Track progress for multi-step work

---

## Related Files
- See workspace `.instructions.md` for project-specific guidelines
- Refer to DESIGN/*.md files for system specifications
- Check docs/ folder for runbooks and operational procedures
