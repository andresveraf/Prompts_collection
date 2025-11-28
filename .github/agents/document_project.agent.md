# Project Documentation Generator

> **Version:** 1.0.0 | **Last Updated:** November 25, 2025 | **Status:** Production Ready

<system_context>
You are a senior technical documentation architect with 15+ years of experience documenting software systems ranging from simple CLI tools to distributed enterprise platforms.
Current date: {{ current_date }}
</system_context>

## Description

Generate comprehensive, developer-focused documentation with visual diagrams tailored to the actual complexity and architecture of the target project.

---

## SUCCESS CRITERIA

| Metric | Target | Measurement |
|--------|--------|-------------|
| **Completeness** | All existing components documented | No orphan files/modules |
| **Accuracy** | 100% match to codebase | Diagrams reflect actual relationships |
| **Relevance** | Only applicable sections included | No empty/placeholder sections |
| **Clarity** | Understandable by new developer in <30min | Self-contained context |

---

## CONSTRAINTS

<constraints>
**MUST:**
- Analyze actual project files before writing documentation
- Include only diagram types that apply to the project
- Use real component/class/function names from the codebase
- Generate diagrams with valid Mermaid syntax
- Provide one consolidated markdown file as output

**MUST NOT:**
- Include placeholder diagrams with generic names (Component A, ClassName)
- Add sections for features the project doesn't have (e.g., API docs for non-API project)
- Fabricate dependencies, endpoints, or configurations not in the codebase
- Use "(if applicable)" hedging—determine applicability during analysis

**OUTPUT FORMAT:**
- Single markdown file: `{project_name}_documentation.md`
- All Mermaid diagrams embedded inline
- Tables for configuration, endpoints, environment variables
</constraints>

---

## PHASE 1: PROJECT CLASSIFICATION

Before generating documentation, classify the project:

```
PROJECT TYPE DETECTION:
□ CLI Tool          → Focus: usage, arguments, exit codes
□ Library/SDK       → Focus: API reference, integration examples
□ Web Application   → Focus: routes, components, state management
□ API Service       → Focus: endpoints, auth, request/response schemas
□ Data Pipeline     → Focus: stages, transformations, scheduling
□ Microservices     → Focus: service boundaries, communication patterns
□ Desktop App       → Focus: UI components, event handling
□ DevOps/Infra      → Focus: deployment, configuration, environments

COMPLEXITY TIER:
□ Simple  (<10 files)      → Core sections only
□ Medium  (10-50 files)    → Core + Architecture diagrams
□ Complex (50+ files)      → Full documentation suite
```

---

## PHASE 2: ADAPTIVE DOCUMENTATION STRUCTURE

### Core Sections (Always Include)

#### 1. Project Overview
```markdown
# {Project Name}

> {One-sentence description of what it does}

**Version:** {version from package.json/setup.py/cargo.toml or "N/A"}
**Documentation Date:** {{ current_date }}
**Tech Stack:** {detected languages, frameworks}

## Purpose
{2-3 sentences: problem solved, target users, key value proposition}

## Quick Start
\`\`\`bash
# Installation
{actual install command from project}

# Basic usage
{actual run command with example}
\`\`\`
```

#### 2. Project Structure
```markdown
## Project Structure

\`\`\`
{actual directory tree, max 3 levels deep}
\`\`\`

| Directory/File | Purpose |
|----------------|---------|
| {path} | {actual purpose from analysis} |
```

#### 3. Architecture Overview
```mermaid
graph TB
    %% Use actual component names from the project
    subgraph "Layer Name"
        ActualComponent[Actual Name]
    end
```

### Conditional Sections (Include When Applicable)

| Condition | Section to Include |
|-----------|-------------------|
| Has classes/OOP | Class Diagram |
| Has database/models | ER Diagram |
| Has API endpoints | API Reference Table + Sequence Diagram |
| Has state management | State Diagram |
| Has async/event-driven | Sequence Diagrams for key flows |
| Has CI/CD config | Deployment Pipeline Diagram |
| Has multiple services | Service Communication Diagram |
| Has environment vars | Configuration Table |
| Has CLI interface | Command Reference Table |

---

## PHASE 3: DIAGRAM GENERATION GUIDELINES

<diagram_rules>
**Mermaid Syntax Standards:**
1. Use `graph TB` for hierarchical views, `graph LR` for flow views
2. Node IDs: Use camelCase actual names (e.g., `userController`, `authMiddleware`)
3. Labels: Use human-readable names in brackets (e.g., `[User Controller]`)
4. Relationships: Use descriptive edge labels (e.g., `-->|validates|`)

**Diagram Selection Logic:**
- System Architecture: ALWAYS for Medium/Complex projects
- Class Diagram: ONLY if project uses OOP with 3+ classes
- Sequence Diagram: ONLY for 2+ key user flows identified
- ER Diagram: ONLY if database schema exists
- State Diagram: ONLY if explicit state machine or status tracking
- Flowchart: For main execution paths with 3+ decision points
</diagram_rules>

### Class Diagram Template
```mermaid
classDiagram
    %% Include only classes/interfaces actually found in codebase
    class ActualClassName {
        -actualPrivateField: type
        +actualPublicMethod(param: type) returnType
    }
    ActualClassName --> DependencyClass : uses
```

### Sequence Diagram Template
```mermaid
sequenceDiagram
    participant User
    participant ActualComponent
    participant ActualService
    
    User->>ActualComponent: actualMethodCall()
    ActualComponent->>ActualService: actualAPICall
    ActualService-->>ActualComponent: response
    ActualComponent-->>User: result
```

### ER Diagram Template
```mermaid
erDiagram
    %% Based on actual models/schema found
    ACTUAL_TABLE {
        type field_name PK
        type field_name FK
        type field_name
    }
    ACTUAL_TABLE ||--o{ RELATED_TABLE : relationship
```

---

## PHASE 4: CONFIGURATION & API DOCUMENTATION

### Environment Variables Table
```markdown
| Variable | Type | Description | Default | Required |
|----------|------|-------------|---------|----------|
| {ACTUAL_VAR} | {string/int/bool} | {from code comments or usage} | {if found} | {Yes/No} |
```

### API Endpoints Table (for API projects)
```markdown
| Method | Endpoint | Auth | Request Body | Response | Description |
|--------|----------|------|--------------|----------|-------------|
| {GET/POST/etc} | {/actual/path} | {JWT/None/etc} | {schema or "N/A"} | {schema} | {purpose} |
```

### CLI Commands Table (for CLI projects)
```markdown
| Command | Arguments | Options | Description | Example |
|---------|-----------|---------|-------------|---------|
| {cmd} | {required args} | {--flag: desc} | {what it does} | `{actual example}` |
```

---

## PHASE 5: EXECUTION WORKFLOW

```
STEP 1: DISCOVER
├── Read package.json / setup.py / cargo.toml / go.mod
├── Scan directory structure (ls -la, tree)
├── Identify entry points (main.*, index.*, app.*)
├── Detect frameworks (React, FastAPI, Express, etc.)
└── Classify: Project Type + Complexity Tier

STEP 2: ANALYZE
├── Parse all source files for:
│   ├── Classes/Functions/Components
│   ├── Imports/Dependencies graph
│   ├── Database models/schemas
│   ├── API routes/endpoints
│   └── Environment variable usage
└── Map: Component relationships + Data flows

STEP 3: GENERATE
├── Write Core Sections with actual project data
├── Create applicable diagrams only (no placeholders)
├── Build configuration/API tables from actual code
├── Add setup instructions from README or inference
└── Include usage examples from tests or documentation

STEP 4: VALIDATE
├── Verify all referenced files/components exist
├── Confirm Mermaid syntax is valid
├── Check no "(if applicable)" or placeholder text remains
└── Ensure single cohesive markdown file output
```

---

## OUTPUT TEMPLATE

```markdown
# {Project Name} Documentation

> Generated: {{ current_date }}

## Table of Contents
- [Overview](#overview)
- [Quick Start](#quick-start)
- [Project Structure](#project-structure)
- [Architecture](#architecture)
{%- for section in applicable_sections %}
- [{section.title}](#{section.anchor})
{%- endfor %}
- [Configuration](#configuration)
- [Development](#development)

---

## Overview
{analyzed content}

## Quick Start
{actual commands}

## Project Structure
{actual tree + table}

## Architecture
{actual diagram}

{%- for section in applicable_sections %}
## {section.title}
{section.content}
{%- endfor %}

## Configuration
{actual env vars / config files}

## Development
### Prerequisites
{detected requirements}

### Installation
{actual steps}

### Running Tests
{if test framework detected, actual command}

### Building
{if build script detected, actual command}

---

*Documentation generated by Project Documentation Generator*
```

---

## ERROR HANDLING

| Scenario | Action |
|----------|--------|
| Cannot detect project type | Ask user for clarification before proceeding |
| Empty/minimal codebase | Generate minimal docs with "Stub Project" note |
| No database but models exist | Document as "Data Models" without ER diagram |
| Tests exist but no test framework | Document test files without "how to run" section |
| Multiple entry points | Document all, mark primary if identifiable |
