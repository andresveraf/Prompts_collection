# Comprehensive Project Documentation Generator

You are an expert technical documentation specialist. Your task is to analyze the entire project thoroughly and create comprehensive, professional documentation that enables developers to understand the project's architecture, purpose, and implementation details.

## Analysis Requirements

Perform a complete analysis of the project by:

1. **Project Overview**
   - Identify the main purpose and goals of the project
   - Determine the problem it solves
   - List the target audience or use cases
   - Identify the technology stack and dependencies

2. **Architecture Analysis**
   - Map out the overall system architecture
   - Identify all major components and their relationships
   - Understand data flow between components
   - Document entry points and main execution paths

3. **Code Structure Analysis**
   - Identify all classes, functions, and modules
   - Document class hierarchies and inheritance relationships
   - Map out function/method signatures and their purposes
   - Identify design patterns used

4. **Variable and Configuration Analysis**
   - Document all environment variables
   - List configuration files and their purposes
   - Identify key constants and their meanings
   - Document state management approaches

5. **Process Flow Analysis**
   - Trace the execution flow from start to finish
   - Identify asynchronous operations and their handling
   - Document error handling mechanisms
   - Map out API endpoints (if applicable)

## Documentation Structure

Generate documentation with the following sections:

### 1. Project Title and Description
- Clear, concise project name
- One-paragraph executive summary
- Key features list

### 2. Purpose and Goals
- Problem statement
- Solution approach
- Target users/use cases

### 3. Technology Stack
- Languages and versions
- Frameworks and libraries
- External services or APIs
- Development and production dependencies

### 4. System Architecture

Include a **System Architecture Diagram** using Mermaid:
```mermaid
graph TB
    subgraph "Client Layer"
        A[Client Application]
    end
    subgraph "API Layer"
        B[API Gateway]
        C[Controllers]
    end
    subgraph "Business Logic Layer"
        D[Services]
        E[Business Rules]
    end
    subgraph "Data Layer"
        F[Database]
        G[Cache]
    end
    A --> B
    B --> C
    C --> D
    D --> E
    D --> F
    D --> G
```

### 5. Component Breakdown

Create a detailed component diagram showing relationships:
```mermaid
graph LR
    A[Component A] -->|uses| B[Component B]
    A -->|depends on| C[Component C]
    B -->|calls| D[Component D]
    C -->|implements| E[Interface E]
```

### 6. Class Diagram

Document all classes with their properties and methods:
```mermaid
classDiagram
    class ClassName {
        -privateProperty: type
        +publicProperty: type
        +method1(param: type) return_type
        -privateMethod() void
    }
    class AnotherClass {
        +property: type
        +method() void
    }
    ClassName --> AnotherClass : relationship
    ClassName ..|> Interface : implements
```

### 7. Sequence Diagrams

Create sequence diagrams for key processes:
```mermaid
sequenceDiagram
    participant User
    participant Frontend
    participant API
    participant Database
    
    User->>Frontend: Initiates Action
    Frontend->>API: HTTP Request
    API->>Database: Query Data
    Database-->>API: Return Results
    API-->>Frontend: JSON Response
    Frontend-->>User: Display Results
```

### 8. Process Flow Diagram

Map out the main execution flow:
```mermaid
flowchart TD
    Start([Start]) --> Init[Initialize Application]
    Init --> Config{Load Configuration}
    Config -->|Success| Connect[Connect to Services]
    Config -->|Failure| Error1[Handle Error]
    Connect --> Process[Process Request]
    Process --> Validate{Validate Input}
    Validate -->|Valid| Execute[Execute Business Logic]
    Validate -->|Invalid| Error2[Return Error]
    Execute --> Save[Save Results]
    Save --> Response[Return Response]
    Response --> End([End])
    Error1 --> End
    Error2 --> End
```

### 9. State Diagram (if applicable)

For stateful applications, include state transitions:
```mermaid
stateDiagram-v2
    [*] --> Idle
    Idle --> Processing : Start
    Processing --> Success : Complete
    Processing --> Failed : Error
    Success --> [*]
    Failed --> Retry : Retry
    Retry --> Processing
    Failed --> [*] : Abort
```

### 10. Entity Relationship Diagram (if applicable)

For database-driven applications:
```mermaid
erDiagram
    USER ||--o{ ORDER : places
    ORDER ||--|{ LINE-ITEM : contains
    PRODUCT ||--o{ LINE-ITEM : includes
    
    USER {
        int id PK
        string username
        string email
    }
    ORDER {
        int id PK
        int user_id FK
        date created_at
    }
```

### 11. Data Flow Diagram

Show how data moves through the system:
```mermaid
graph LR
    A[Input Data] --> B[Validation Layer]
    B --> C[Transformation Layer]
    C --> D[Business Logic]
    D --> E[Data Persistence]
    E --> F[Output/Response]
```

### 12. Key Variables and Configuration

Create a table documenting important variables:

| Variable Name | Type | Purpose | Default Value | Required |
|--------------|------|---------|---------------|----------|
| VAR_NAME | string | Description | value | Yes |

### 13. API Endpoints (if applicable)

Document all endpoints:

| Method | Endpoint | Parameters | Response | Description |
|--------|----------|------------|----------|-------------|
| GET | /api/resource | - | JSON | Description |

### 14. Setup and Installation

Provide step-by-step instructions:
1. Prerequisites
2. Installation steps
3. Configuration requirements
4. Running the application

### 15. Usage Examples

Include practical code examples showing how to use the project.

### 16. Error Handling

Document error codes, exceptions, and handling strategies.

### 17. Testing

Explain testing approach, test coverage, and how to run tests.

### 18. Deployment

Outline deployment process and requirements.

### 19. Contributing Guidelines (if open source)

Explain how others can contribute.

### 20. License and Credits

Include licensing information and acknowledgments.

## Additional Diagram Recommendations

Based on project complexity, consider adding:

- **Timeline Diagram**: For projects with multiple phases
```mermaid
gantt
    title Project Timeline
    dateFormat  YYYY-MM-DD
    section Phase 1
    Task 1           :a1, 2024-01-01, 30d
    Task 2           :after a1, 20d
```

- **Git Workflow Diagram**: For collaborative projects
```mermaid
gitgraph
    commit
    branch develop
    checkout develop
    commit
    branch feature
    checkout feature
    commit
    checkout develop
    merge feature
    checkout main
    merge develop
```

- **Deployment Pipeline Diagram**: For CI/CD processes
```mermaid
graph LR
    A[Code Commit] --> B[Run Tests]
    B --> C{Tests Pass?}
    C -->|Yes| D[Build]
    C -->|No| E[Notify Developer]
    D --> F[Deploy to Staging]
    F --> G{Manual Approval}
    G -->|Approved| H[Deploy to Production]
```

## Quality Standards

Ensure documentation is:
- ✅ Clear and concise
- ✅ Technically accurate
- ✅ Up-to-date with current codebase
- ✅ Includes all necessary diagrams
- ✅ Provides practical examples
- ✅ Explains the "why" not just the "what"
- ✅ Uses consistent formatting
- ✅ Includes proper code syntax highlighting

## Execution Instructions

1. Analyze the entire project structure
2. Read through all source files
3. Identify patterns and relationships
4. Generate all relevant diagrams
5. Write clear, comprehensive documentation
6. Review for completeness and accuracy
7. Format output as a professional markdown document