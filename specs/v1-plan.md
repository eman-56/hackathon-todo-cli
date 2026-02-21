# V1 Architecture Plan

## System Overview

The Phase I Todo CLI Application follows a **modular layered architecture** with clear separation of concerns:

```
┌─────────────────────────────────────────┐
│           CLI Layer (cli.py)            │
│  - Command parsing                      │
│  - User interaction                     │
│  - Output formatting                    │
└─────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────┐
│        Service Layer (services/)        │
│  - TaskService: Business logic          │
│  - In-memory task management            │
└─────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────┐
│         Model Layer (models/)           │
│  - Task: Data structure                 │
│  - TaskStatus: Enum (PENDING/COMPLETE)  │
└─────────────────────────────────────────┘
```

## Key Architectural Decisions

### 1. Modular File Structure
**Decision**: Separate files for models, services, and CLI

**Rationale**:
- Aligns with Constitution Principle II (Simple Design)
- Enables independent testing of each layer
- Clear boundaries for future extensions

**Trade-offs**:
- More files than a single-file solution
- Justified by testability and maintainability

### 2. In-Memory Storage with Service Abstraction
**Decision**: Use a service layer even for simple in-memory storage

**Rationale**:
- Enables future storage backend swaps (file, database) without CLI changes
- Business logic isolated from data access
- Easier to mock for testing

**Trade-offs**:
- Slight over-engineering for v1
- Mitigated by simple implementation

### 3. Text-Based CLI Interface
**Decision**: Simple argparse-based CLI with subcommands

**Rationale**:
- Aligns with Constitution Principle IV (Observable by Default)
- Easy to debug and test
- No external dependencies

**Commands**:
- `todo add <title> [--description <desc>]`
- `todo list`
- `todo update <id> [--title <title>] [--description <desc>]`
- `todo delete <id>`
- `todo complete <id>`
- `todo incomplete <id>`

## Data Model

### Task
```python
class Task:
    id: int           # Auto-incremented
    title: str        # Required
    description: str  # Optional, default ""
    status: TaskStatus # PENDING or COMPLETE
    created_at: datetime
```

### TaskStatus (Enum)
```python
class TaskStatus(Enum):
    PENDING = "pending"
    COMPLETE = "complete"
```

## Component Responsibilities

### models/task.py
- Task dataclass
- TaskStatus enum
- Validation logic

### services/task_service.py
- TaskService class
- In-memory storage (list/dict)
- CRUD operations: add, get, list, update, delete
- Status toggle methods
- ID generation

### cli.py
- argparse setup
- Command routing
- Input validation
- Output formatting
- Error handling

## Error Handling Strategy

| Error Type | Handling |
|------------|----------|
| Task not found | Return error message, exit code 1 |
| Invalid ID | Validate, show helpful message |
| Missing required args | argparse handles automatically |
| Empty task list | Show friendly message |

## Testing Strategy

Following Constitution Principle I (Test-First):

1. **Unit Tests** (`tests/unit/`):
   - Task model creation
   - TaskService CRUD operations
   - Status transitions

2. **Integration Tests** (`tests/integration/`):
   - CLI command parsing
   - End-to-end workflows

3. **Test Commands**:
   - `pytest tests/` - Run all tests
   - `pytest tests/unit/` - Unit only
   - `pytest tests/integration/` - Integration only

## File Structure

```
project/
├── cli.py              # Main entry point
├── models/
│   ├── __init__.py
│   └── task.py         # Task dataclass, TaskStatus enum
├── services/
│   ├── __init__.py
│   └── task_service.py # TaskService class
├── tests/
│   ├── __init__.py
│   ├── unit/
│   │   ├── __init__.py
│   │   ├── test_task.py
│   │   └── test_task_service.py
│   └── integration/
│       ├── __init__.py
│       └── test_cli.py
├── requirements.txt    # Empty or minimal
└── README.md           # Usage instructions
```

## Implementation Order

1. **Models** - Task data structure
2. **Services** - Business logic
3. **CLI** - User interface
4. **Tests** - Alongside each layer (test-first)

## Success Criteria

- [ ] All 5 functional requirements implemented
- [ ] All tests passing
- [ ] CLI commands work as specified
- [ ] Code follows constitution principles
- [ ] No external dependencies required

---

**Version**: 1.0.0  
**Created**: 2026-02-21  
**Status**: Ready for Implementation
