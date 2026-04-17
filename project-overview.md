# PES-VCS Project Overview

## Student Details
Name: Ahana Srinivas  
USN: PES1UG24CS910  
Course: Operating Systems Lab

---

## Project Snapshot
PES-VCS is a lightweight version control system implemented in C to model the core internal behavior of Git-style tools.

The design stores complete repository snapshots using hash-addressed objects instead of traditional diff files. This keeps the model simple, verifiable, and aligned with operating systems concepts such as persistent state, file layout, and metadata handling.

---

## Objectives
- Build a content-addressable object store using SHA-256
- Represent directory structure through tree objects
- Maintain a staging area (index) for controlled snapshot creation
- Record commit history using parent-linked commit objects
- Provide a CLI workflow with init, add, status, commit, and log

---

## System Design
PES-VCS separates responsibilities into focused modules:

- object.c: stores and retrieves immutable objects by hash
- tree.c: converts staged paths into deterministic tree snapshots
- index.c: reads, updates, and writes the staging index
- commit.c: creates commit objects and walks commit history
- pes.c: command routing and user-facing command behavior

This structure keeps storage logic, snapshot building, and history traversal independent and testable.

---

## Storage Model
The implementation follows three core object types:

1. Blob
Contains raw file bytes.

2. Tree
Represents directory entries and points to blobs/child trees.

3. Commit
References a root tree, optional parent commit, author/metadata, and message.

Repository references are maintained under .pes/refs, with HEAD tracking the active branch reference.

---

## Phase-wise Implementation Summary

### Phase 1: Object Layer
- Implemented object hashing and object persistence
- Added object read/write validation
- Verified sharded object path behavior through tests

### Phase 2: Tree Construction
- Built tree generation from staged file entries
- Supported nested paths and reproducible tree output
- Validated tree object structure via test cases

### Phase 3: Index and Status
- Implemented index load/save/add operations
- Added staging flow for file tracking
- Enabled status output from index and working state

### Phase 4: Commit and Log
- Implemented commit creation and metadata serialization
- Linked commits through parent pointers
- Added history traversal through log command

---

## Build and Validation

### Build
- make
- make all
- make clean

### Unit Tests
- ./test_objects
- ./test_tree

### Integration Test
- make test-integration
- ./test_sequence.sh

---

## Typical Workflow
- ./pes init
- ./pes add <path>
- ./pes status
- ./pes commit -m "message"
- ./pes log

---

## Deliverables for Submission
- Source files for object, tree, index, and commit modules
- Screenshots for all required checkpoints across phases
- report.pdf at repository root containing screenshots and analysis answers
- A clear commit history showing incremental work

---

## Repository Contents (Key Files)
- object.c
- tree.c
- index.c
- commit.c
- pes.c
- Makefile
- test_objects.c
- test_tree.c
- test_sequence.sh
- report.pdf
- README.md

---

## Closing Note
This project focuses on correctness of storage semantics and commit-chain behavior rather than broad feature coverage. It serves as a practical systems-level foundation for understanding how real VCS engines manage integrity, history, and reproducibility.
