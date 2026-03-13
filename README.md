# OpenCode Configuration: Agent Orchestration Setup

This directory contains a specialized OpenCode configuration optimized for coordinated multi-agent development workflows with external documentation and code search capabilities.

## Overview

This configuration disables OpenCode's default agents in favor of a concise multi-agent setup with specialized agents and shared research tools. The setup integrates two MCP (Model Context Protocol) servers to provide access to external documentation and real-world code examples.

## Configuration Details

### Disabled Default Agents

The following OpenCode default agents are disabled in `opencode.json`:

- **plan**: Default planning agent
- **build**: Default build/implementation agent  
- **general**: General-purpose agent

**Rationale**: These agents are replaced by a custom agent set that separates orchestration, investigation, implementation, testing, security review, planning, and general Q&A.

### MCP Servers

#### context7
- **URL**: `https://mcp.context7.com/mcp`
- **Purpose**: Provides access to up-to-date documentation and library references for various programming frameworks and libraries
- **Use Cases**: 
  - Looking up API documentation
  - Checking library references
  - Verifying framework conventions
  - Researching best practices

#### gh_grep
- **URL**: `https://mcp.grep.app`
- **Purpose**: Searches real-world code examples from over a million public GitHub repositories
- **Use Cases**:
  - Finding implementation patterns
  - Seeing how others solved similar problems
  - Learning idiomatic code patterns
  - Reference implementations

## Agent Architecture

### Agent Inventory

**orchestrate**
- **Mode**: Primary
- **Role**: Central coordinator for complex development workflows
- **Focus**: Plan execution, delegate work, validate outcomes

**inspect**
- **Mode**: Primary
- **Role**: Deep code analysis and architecture explanation
- **Constraints**: Read-only (no code modifications)

**design**
- **Mode**: Primary
- **Role**: Requirements, architecture, and implementation planning

**atlas**
- **Mode**: All
- **Role**: Broad question-answering, practical guidance, and research-heavy explanations

### Subagents

**implement**
- **Mode**: Subagent
- **Role**: Write clean, production-quality code

**debug**
- **Mode**: Subagent
- **Role**: Diagnose and fix bugs, errors, and unexpected behavior

**secure**
- **Mode**: Subagent
- **Role**: Review code for vulnerabilities and security best practices
- **Trigger Points**:
  - Before deploying authentication/authorization features
  - After changes to security-critical areas
  - When handling user input, external APIs, or sensitive data

**test**
- **Mode**: Subagent
- **Role**: Execute tests, generate coverage, verify functionality

## Skills

### backend-engineering
- **Path**: `skill/backend-engineering/SKILL.md`
- **Focus**: Production-grade backend systems
- **Principles**:
  - Correctness first, performance second
  - Explicit over clever
  - Defensive programming
  - Full observability

### frontend-design
- **Path**: `skill/frontend-design/SKILL.md`
- **Focus**: Production-grade frontend interfaces
- **Approach**: High design quality with creative, polished code

### system-engineer
- **Path**: `skill/system-engineer/SKILL.md`
- **Focus**: Production-grade infrastructure and cloud systems
- **Principles**:
  - Cost-aware design to avoid wasteful spending
  - Resilient architecture with failure recovery
  - Observable systems with proper monitoring
  - Reproducible infrastructure as code
  - Security-first approach

## Workflow Pattern

### Standard Development Workflow

1. **User Request**: User describes desired functionality or problem
2. **Orchestration**: orchestrate analyzes requirements
3. **Delegation**: Orchestrator delegates to appropriate subagents:
    - implement for new code/changes
    - debug if issues reported
    - secure for sensitive features
    - test for verification
    - design when upfront requirements/design work is needed
4. **Validation**: Orchestrator validates subagent outputs
5. **Iteration**: If issues found, orchestrator re-delegates with feedback
6. **Completion**: Orchestrator verifies all requirements met and provides summary

### Investigation Workflow

1. **User Query**: User asks about codebase architecture or behavior
2. **Investigation**: inspect analyzes relevant code
3. **Research**: Uses MCP servers for documentation and patterns
4. **Reporting**: Provides structured explanation with code references

### Using MCP Servers

**context7 Usage**:
```
Query: "How to set up authentication with JWT in Express.js"
```

**gh_grep Usage**:
```
Query: "useState loading state example TypeScript"
```

Both servers are automatically available to all agents for research and reference.

## Directory Structure

```
opencode/
├── opencode.json
├── agent/
│   ├── atlas.md
│   ├── orchestrate.md
│   ├── debug.md
│   ├── design.md
│   ├── implement.md
│   ├── inspect.md
│   ├── secure.md
│   └── test.md
├── skill/
│   ├── backend-engineering/SKILL.md
│   ├── frontend-design/SKILL.md
│   └── system-engineer/SKILL.md
└── README.md
```

## Key Benefits

1. **Specialization**: Each agent has a narrow, clear role
2. **Coordination**: orchestrate manages multi-step engineering work
3. **Coverage**: atlas, inspect, design, implement, debug, secure, and test cover research through verification
4. **External Knowledge**: MCP servers provide current documentation and real-world patterns

## Interaction Pattern

When working with this setup:

1. **For new features/bug fixes**: orchestrate coordinates the workflow
2. **For code questions**: inspect analyzes and explains
3. **For planning/design work**: design defines requirements and architecture
4. **For broad Q&A or research**: atlas answers directly or goes deep
5. **For implementation, security, and verification**: implement, secure, and test handle execution

All agents have access to context7 (documentation) and gh_grep (code examples) for research.

## Notes

- This configuration is designed for complex, production-quality development workflows
- The orchestrator pattern ensures comprehensive quality gates
- MCP servers are read-only and used for research purposes only
- All agents follow the principles defined in the skill files for their domain
