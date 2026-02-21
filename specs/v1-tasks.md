# V1 Task Breakdown

## Implementation Tasks

### Task 1: Project Setup
**Category**: Setup  
**Priority**: P0

**Description**: Initialize project structure with directories and base files

**Subtasks**:
- [ ] Create `models/` directory with `__init__.py`
- [ ] Create `services/` directory with `__init__.py`
- [ ] Create `tests/` directory with `__init__.py`
- [ ] Create `tests/unit/` directory with `__init__.py`
- [ ] Create `tests/integration/` directory with `__init__.py`
- [ ] Create empty `requirements.txt`
- [ ] Create basic `README.md` with usage

**Test Cases**:
- [ ] Directory structure exists
- [ ] Python can import from all packages

---

### Task 2: Task Model
**Category**: Models  
**Priority**: P0  
**Spec Reference**: FR-1, FR-2, FR-3, FR-4, FR-5

**Description**: Create the Task dataclass and TaskStatus enum

**Subtasks**:
- [ ] Define TaskStatus enum (PENDING, COMPLETE)
- [ ] Define Task dataclass with id, title, description, status, created_at
- [ ] Add validation for required fields
- [ ] Add string representation for debugging

**Test Cases**:
- [ ] T2.1: Create task with minimal fields (id, title)
- [ ] T2.2: Create task with all fields
- [ ] T2.3: Task status defaults to PENDING
- [ ] T2.4: Task string representation includes key fields
- [ ] T2.5: TaskStatus enum values are correct

**Files**: `models/task.py`

---

### Task 3: Task Service
**Category**: Services  
**Priority**: P0  
**Spec Reference**: FR-1, FR-2, FR-3, FR-4, FR-5

**Description**: Implement TaskService with in-memory storage and CRUD operations

**Subtasks**:
- [ ] Create TaskService class
- [ ] Implement in-memory storage (list or dict)
- [ ] Implement `add_task(title, description)` → Task
- [ ] Implement `get_task(id)` → Task | None
- [ ] Implement `list_tasks()` → list[Task]
- [ ] Implement `update_task(id, title?, description?)` → Task | None
- [ ] Implement `delete_task(id)` → bool
- [ ] Implement `complete_task(id)` → Task | None
- [ ] Implement `incomplete_task(id)` → Task | None
- [ ] Implement auto-increment ID generation

**Test Cases**:
- [ ] T3.1: Add task returns task with auto-generated ID
- [ ] T3.2: Get existing task returns task
- [ ] T3.3: Get non-existent task returns None
- [ ] T3.4: List tasks returns all tasks
- [ ] T3.5: Update task modifies fields
- [ ] T3.6: Update non-existent task returns None
- [ ] T3.7: Delete task removes from storage
- [ ] T3.8: Delete non-existent task returns False
- [ ] T3.9: Complete task changes status to COMPLETE
- [ ] T3.10: Incomplete task changes status to PENDING
- [ ] T3.11: IDs are unique and auto-incremented

**Files**: `services/task_service.py`

---

### Task 4: CLI - Add Command
**Category**: CLI  
**Priority**: P0  
**Spec Reference**: FR-1

**Description**: Implement `todo add` command

**Subtasks**:
- [ ] Create cli.py with argparse setup
- [ ] Add `add` subcommand with title (positional) and --description (optional)
- [ ] Call TaskService.add_task()
- [ ] Print confirmation with task ID
- [ ] Handle errors gracefully

**Test Cases**:
- [ ] T4.1: `todo add "My Task"` creates task
- [ ] T4.2: `todo add "Task" --description "Desc"` creates task with description
- [ ] T4.3: Output shows task ID and title
- [ ] T4.4: Missing title shows error

**Files**: `cli.py`

---

### Task 5: CLI - List Command
**Category**: CLI  
**Priority**: P0  
**Spec Reference**: FR-2

**Description**: Implement `todo list` command

**Subtasks**:
- [ ] Add `list` subcommand
- [ ] Call TaskService.list_tasks()
- [ ] Format output with ID, title, description, status indicator
- [ ] Handle empty list gracefully

**Test Cases**:
- [ ] T5.1: `todo list` shows all tasks
- [ ] T5.2: Output includes status indicators ([ ] / [x])
- [ ] T5.3: Empty list shows friendly message

**Files**: `cli.py`

---

### Task 6: CLI - Update Command
**Category**: CLI  
**Priority**: P1  
**Spec Reference**: FR-3

**Description**: Implement `todo update` command

**Subtasks**:
- [ ] Add `update` subcommand with id (positional)
- [ ] Add --title and --description optional arguments
- [ ] Call TaskService.update_task()
- [ ] Print confirmation or error

**Test Cases**:
- [ ] T6.1: `todo update 1 --title "New Title"` updates title
- [ ] T6.2: `todo update 1 --description "New Desc"` updates description
- [ ] T6.3: Update non-existent ID shows error
- [ ] T6.4: Update with no changes shows message

**Files**: `cli.py`

---

### Task 7: CLI - Delete Command
**Category**: CLI  
**Priority**: P1  
**Spec Reference**: FR-4

**Description**: Implement `todo delete` command

**Subtasks**:
- [ ] Add `delete` subcommand with id (positional)
- [ ] Call TaskService.delete_task()
- [ ] Print confirmation or error

**Test Cases**:
- [ ] T7.1: `todo delete 1` removes task
- [ ] T7.2: Delete non-existent ID shows error

**Files**: `cli.py`

---

### Task 8: CLI - Complete/Incomplete Commands
**Category**: CLI  
**Priority**: P1  
**Spec Reference**: FR-5

**Description**: Implement `todo complete` and `todo incomplete` commands

**Subtasks**:
- [ ] Add `complete` subcommand with id (positional)
- [ ] Add `incomplete` subcommand with id (positional)
- [ ] Call respective TaskService methods
- [ ] Print confirmation or error

**Test Cases**:
- [ ] T8.1: `todo complete 1` marks task complete
- [ ] T8.2: `todo incomplete 1` marks task incomplete
- [ ] T8.3: Commands on non-existent ID show error

**Files**: `cli.py`

---

### Task 9: Entry Point Setup
**Category**: Setup  
**Priority**: P0

**Description**: Make CLI executable as module and script

**Subtasks**:
- [ ] Add `if __name__ == "__main__":` block in cli.py
- [ ] Create `__main__.py` for `python -m` execution
- [ ] Test both execution methods

**Test Cases**:
- [ ] T9.1: `python cli.py --help` works
- [ ] T9.2: `python -m cli --help` works (if __main__.py created)

**Files**: `cli.py`, `__main__.py` (optional)

---

### Task 10: Integration Tests
**Category**: Testing  
**Priority**: P1

**Description**: Write integration tests for full workflows

**Subtasks**:
- [ ] Test add → list → verify
- [ ] Test add → update → list → verify
- [ ] Test add → complete → list → verify
- [ ] Test add → delete → list → verify
- [ ] Test full workflow with multiple tasks

**Test Cases**:
- [ ] T10.1: Full CRUD workflow
- [ ] T10.2: Status toggle workflow
- [ ] T10.3: Multiple tasks with different statuses

**Files**: `tests/integration/test_cli.py`

---

### Task 11: README Documentation
**Category**: Documentation  
**Priority**: P2

**Description**: Complete README with usage examples

**Subtasks**:
- [ ] Add project description
- [ ] Add installation instructions
- [ ] Add all CLI command examples
- [ ] Add development/setup instructions

**Files**: `README.md`

---

## Task Summary

| ID | Task | Category | Priority | Est. Tests |
|----|------|----------|----------|------------|
| 1 | Project Setup | Setup | P0 | 2 |
| 2 | Task Model | Models | P0 | 5 |
| 3 | Task Service | Services | P0 | 11 |
| 4 | CLI - Add | CLI | P0 | 4 |
| 5 | CLI - List | CLI | P0 | 3 |
| 6 | CLI - Update | CLI | P1 | 4 |
| 7 | CLI - Delete | CLI | P1 | 2 |
| 8 | CLI - Complete/Incomplete | CLI | P1 | 3 |
| 9 | Entry Point | Setup | P0 | 2 |
| 10 | Integration Tests | Testing | P1 | 3 |
| 11 | README | Documentation | P2 | 0 |

**Total**: 11 tasks, ~39 test cases

---

**Created**: 2026-02-21  
**Status**: Ready for Implementation
