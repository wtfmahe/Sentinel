# Sentinel Architecture

Version: 1.0
Status: Draft
Last Updated: 2026-06-25

---

# Purpose

This document defines the technical architecture of Sentinel.

It describes every major subsystem, how they interact, and the engineering principles that guide implementation.

This document is the single source of truth for the platform architecture.

---

# High-Level Architecture

```
                    User
                      │
                      ▼
               Next.js Dashboard
                      │
                      ▼
                API Gateway (NestJS)
                      │
        ┌─────────────┼─────────────┐
        ▼             ▼             ▼

   Agent Engine   Memory Engine   Task Engine
        │             │             │
        └──────┬──────┴──────┬──────┘
               ▼             ▼
          Tool Engine     Scheduler
               │
     ┌─────────┼──────────────┐
     ▼         ▼              ▼

 Browser    LLM Tool     Filesystem
 Git        Search       Email
 Storage    Calendar     Excel

               │
               ▼

          Supabase
      PostgreSQL + Storage

               │
               ▼

        Redis + BullMQ
```

---

# Core Architecture

Sentinel consists of six independent engines.

1. Agent Engine
2. Tool Engine
3. Memory Engine
4. Task Engine
5. Scheduler
6. API Gateway

Each engine has one responsibility.

---

# Engine 1 — Agent Engine

## Responsibility

Execute intelligent workflows.

Agents never directly communicate with:

* Database
* Browser
* LLM
* Filesystem

Agents only communicate with Tools.

---

## Responsibilities

* Load agents
* Register agents
* Execute agents
* Manage lifecycle
* Agent permissions
* Agent discovery

---

## Example Agents

* Job Agent
* Coding Agent
* Research Agent
* Browser Agent
* GitHub Agent
* Email Agent
* Calendar Agent

---

# Agent Lifecycle

Every agent follows exactly the same lifecycle.

```
Receive Task

↓

Read Memory

↓

Plan

↓

Invoke Tools

↓

Evaluate Result

↓

Update Memory

↓

Complete Task
```

---

# Engine 2 — Tool Engine

## Responsibility

Provide reusable capabilities.

Every external interaction happens through a Tool.

---

## Initial Tools

Browser Tool

LLM Tool

Memory Tool

Filesystem Tool

Git Tool

Search Tool

Email Tool

Calendar Tool

Excel Tool

Notification Tool

---

## Tool Interface

Every Tool must implement:

```
initialize()

execute()

validate()

cleanup()
```

Tools are stateless.

---

# Engine 3 — Memory Engine

Memory is Sentinel's foundation.

Conversation history is NOT memory.

Memory is structured knowledge.

---

## Stores

User Profile

Projects

Skills

Experiences

Preferences

Documents

Goals

Tasks

Application History

Conversation Summaries

Knowledge

Relationships

---

## Responsibilities

Store

Retrieve

Update

Summarize

Search

Version

---

# Memory Types

## User Memory

Who the user is.

---

## Semantic Memory

Facts.

Knowledge.

Relationships.

---

## Episodic Memory

Past executions.

Failures.

Successes.

Previous reasoning.

---

## Task Memory

Running tasks.

Completed tasks.

Logs.

Results.

---

# Engine 4 — Task Engine

Everything becomes a Task.

Examples

Search Jobs

Apply Job

Generate Resume

Research Company

Commit Code

Read Email

---

## Task Lifecycle

Created

↓

Queued

↓

Assigned

↓

Running

↓

Completed

↓

Archived

---

# Engine 5 — Scheduler

Scheduler creates Tasks.

Examples

Every hour

Every morning

Every Monday

When event happens

When webhook received

---

Scheduler never executes work.

It only creates Tasks.

---

# Engine 6 — API Gateway

Single entry point.

Responsibilities

Authentication

Authorization

REST APIs

WebSockets

Rate Limiting

Validation

Health Checks

---

# Repository Structure

```
Sentinel/

apps/

    api/

    web/

    worker/

packages/

    agents/

    tools/

    memory/

    database/

    sdk/

    shared/

    config/

    ui/

docs/

docker/

scripts/

examples/
```

---

# Communication Rules

Agents never communicate directly.

```
Agent

↓

Task Engine

↓

Tool

↓

Memory
```

No shortcuts.

---

# Data Flow

```
Goal

↓

Planner

↓

Tasks

↓

Scheduler

↓

Queue

↓

Agent

↓

Tool

↓

Result

↓

Memory Updated
```

---

# Queue

Redis

BullMQ

Responsibilities

Retry

Priority

Scheduling

Concurrency

Dead Letter Queue

---

# Database

Supabase

Responsibilities

Authentication

Storage

PostgreSQL

Realtime

Future Vector Search

---

# Authentication

Supabase Auth

Initial providers

Email

Password

Future

Google

GitHub

Microsoft

---

# Frontend

Next.js

Responsibilities

Dashboard

Tasks

Agents

Memory

Logs

Settings

Notifications

---

# Backend

NestJS

Responsibilities

API

Authentication

Business Logic

Task Management

Memory Access

Agent Registry

---

# Worker

Dedicated background service.

Responsibilities

Execute Tasks

Run Agents

Process Queue

Update Memory

Log Results

---

# Logging

Every execution produces logs.

Every log contains

Timestamp

Task

Agent

Duration

Status

Result

Errors

---

# Plugin System

Sentinel is plugin-first.

Agents register themselves.

Tools register themselves.

Platform discovers them automatically.

---

# Guiding Rules

Platform never knows business logic.

Agents never access databases directly.

Agents never call external APIs directly.

Everything goes through Tools.

Everything important is stored in Memory.

Every execution becomes a Task.

Every subsystem is replaceable.

---

# Technology Stack

Frontend

Next.js

Backend

NestJS

Database

Supabase

Authentication

Supabase Auth

Storage

Supabase Storage

Queue

BullMQ

Cache

Redis

Browser Automation

Playwright

AI

Azure OpenAI

Package Manager

pnpm

Monorepo

Turborepo

---

# Scalability Goals

Support multiple users.

Support multiple agents.

Support multiple workers.

Support distributed execution.

Support plugin marketplace.

Support multiple LLM providers.

Support cloud deployment.

Support self-hosted deployment.

---

# Architecture Principles

Single Responsibility.

Loose Coupling.

High Cohesion.

Replaceable Components.

Configuration over Hardcoding.

Memory First.

Tool Driven.

Plugin Based.

Documentation Driven.

---

# Future Architecture

Future versions may introduce

* Distributed Workers
* Agent Marketplace
* Tool Marketplace
* Voice Interface
* Mobile Applications
* Desktop Client
* Enterprise Deployment
* Multi-Tenant Support
* Vector Memory
* Knowledge Graph
* Event Bus

without changing the core architecture defined in this document.

---

# Version History

Version 1.0

Initial architecture specification establishing the engines, communication model, repository structure, execution lifecycle, and guiding engineering principles for Sentinel.

