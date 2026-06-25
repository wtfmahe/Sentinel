# Sentinel Database Design

Version: 1.0
Status: Draft
Last Updated: 2026-06-25

---

# Purpose

This document defines the logical database architecture for Sentinel.

The database stores users, goals, tasks, memory, agents, tools, executions, and logs.

The implementation will use Supabase (PostgreSQL), but the design remains database-agnostic.

---

# Design Principles

The database should be:

* Normalized where appropriate
* Easy to extend
* Auditable
* Versioned
* Secure
* Performant

---

# Core Entities

Sentinel is built around these primary entities:

* User
* Goal
* Task
* Agent
* Tool
* Memory
* Execution
* Notification

---

# User

Represents an authenticated Sentinel user.

Stores:

* Profile
* Preferences
* Authentication Reference
* Settings

---

# Goal

Represents something the user wants to accomplish.

Examples:

* Get a Software Engineering job
* Learn Rust
* Build Sentinel
* Publish a portfolio

Goals generate Tasks.

---

# Task

Represents a unit of work.

Examples:

* Search LinkedIn
* Generate Resume
* Apply to Company
* Send Email

Each Task belongs to exactly one Goal.

---

# Agent

Represents a registered autonomous agent.

Stores:

* Name
* Version
* Capabilities
* Status
* Configuration

---

# Tool

Represents a registered tool.

Stores:

* Name
* Category
* Version
* Permissions
* Configuration

---

# Memory

Stores long-term knowledge.

Each memory entry contains:

* Type
* Content
* Summary
* Metadata
* Version
* Created Time
* Updated Time

---

# Execution

Represents one execution of an Agent.

Stores:

* Task
* Agent
* Start Time
* End Time
* Status
* Logs
* Errors

---

# Notification

Stores notifications sent to users.

Examples:

* Job Applied
* Task Failed
* Memory Updated
* Goal Completed

---

# Relationships

```text
User
 │
 ├── Goals
 │      │
 │      ├── Tasks
 │      │      │
 │      │      ├── Executions
 │      │      └── Logs
 │      │
 │      └── Memory
 │
 ├── Notifications
 │
 └── Preferences
```

---

# Audit Fields

Every table should include:

* id
* created_at
* updated_at
* created_by
* updated_by

Soft deletion may be introduced later.

---

# Indexing

Indexes should exist for:

* User ID
* Goal ID
* Task ID
* Memory Type
* Execution Status
* Created Time

---

# Security

The database should support:

* Row-Level Security
* Encrypted Secrets
* Audit Logging
* Permission Isolation

---

# Future Tables

Future versions may introduce:

* Plugin
* Workflow
* Team
* Organization
* Billing
* Marketplace

without changing the core schema.

---

# Success Criteria

The database should support millions of tasks, memory records, and executions while maintaining fast retrieval and clear relationships between all entities.

---

# Version History

Version 1.0

Initial logical database design for Sentinel.

