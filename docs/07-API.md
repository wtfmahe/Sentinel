# Sentinel API Specification

Version: 1.0
Status: Draft
Last Updated: 2026-06-25

---

# Purpose

This document defines the public API exposed by Sentinel.

The API provides access to users, goals, tasks, memory, agents, tools, executions, and notifications.

The backend implementation will use NestJS.

---

# Design Principles

The API should be:

* RESTful
* Versioned
* Stateless
* Secure
* Documented
* Consistent

---

# Base URL

```
/api/v1
```

Future versions may introduce:

```
/api/v2
```

---

# Authentication

Authentication uses Supabase Auth.

Supported providers:

* Email
* Google
* GitHub
* Microsoft

Every protected endpoint requires a valid JWT.

---

# Users

## Get Current User

GET

```
/users/me
```

---

## Update Profile

PATCH

```
/users/me
```

---

# Goals

## List Goals

GET

```
/goals
```

---

## Create Goal

POST

```
/goals
```

---

## Update Goal

PATCH

```
/goals/{id}
```

---

## Delete Goal

DELETE

```
/goals/{id}
```

---

# Tasks

## List Tasks

GET

```
/tasks
```

---

## Get Task

GET

```
/tasks/{id}
```

---

## Create Task

POST

```
/tasks
```

---

## Cancel Task

POST

```
/tasks/{id}/cancel
```

---

# Agents

## List Agents

GET

```
/agents
```

---

## Get Agent

GET

```
/agents/{id}
```

---

## Execute Agent

POST

```
/agents/{id}/execute
```

---

# Tools

## List Tools

GET

```
/tools
```

---

## Get Tool

GET

```
/tools/{id}
```

---

# Memory

## Search Memory

GET

```
/memory/search
```

---

## Get Memory

GET

```
/memory/{id}
```

---

## Create Memory

POST

```
/memory
```

---

## Update Memory

PATCH

```
/memory/{id}
```

---

# Executions

## List Executions

GET

```
/executions
```

---

## Get Execution

GET

```
/executions/{id}
```

---

# Notifications

## List Notifications

GET

```
/notifications
```

---

## Mark Read

POST

```
/notifications/{id}/read
```

---

# Health

## Health Check

GET

```
/health
```

---

## Metrics

GET

```
/metrics
```

---

# Error Format

Every error should return:

* Status Code
* Error Code
* Message
* Timestamp
* Request ID

---

# Success Format

Every successful response should include:

* Data
* Metadata
* Pagination (when applicable)

---

# Versioning

Breaking changes require a new API version.

Minor additions should remain backward compatible.

---

# Security

Every endpoint should support:

* Authentication
* Authorization
* Validation
* Rate Limiting
* Audit Logging

---

# Future APIs

Future versions may expose:

* GraphQL
* WebSockets
* Server Sent Events
* Public Plugin API

---

# Success Criteria

The API should provide a consistent interface for all Sentinel clients while remaining extensible for future versions.

---

# Version History

Version 1.0

Initial API specification.

