# Sentinel Coding Standards

Version: 1.0
Status: Draft
Last Updated: 2026-06-25

---

# Purpose

This document defines the coding standards for the Sentinel project.

The goal is to maintain a clean, consistent, scalable, and maintainable codebase.

---

# General Principles

Code should be:

* Simple
* Readable
* Modular
* Testable
* Documented
* Consistent

Always optimize for maintainability over cleverness.

---

# Repository Structure

Applications belong in:

apps/

Shared code belongs in:

packages/

Documentation belongs in:

docs/

Scripts belong in:

scripts/

---

# Naming

Folders:

kebab-case

Examples:

agent-engine

memory-service

browser-tool

Files:

kebab-case

Classes:

PascalCase

Interfaces:

PascalCase

Functions:

camelCase

Variables:

camelCase

Constants:

UPPER_SNAKE_CASE

---

# TypeScript

Always use strict mode.

Avoid `any`.

Prefer interfaces for contracts.

Prefer explicit return types on public APIs.

---

# Functions

Functions should:

* Have one responsibility
* Be small
* Be reusable
* Avoid side effects

---

# Classes

Classes should:

* Have one responsibility
* Prefer dependency injection
* Avoid global state

---

# Logging

Never use console.log in production code.

Use the project logging service.

Every error should include:

* Timestamp
* Context
* Request ID
* Stack Trace (where applicable)

---

# Error Handling

Never swallow exceptions.

Always return meaningful error messages.

Retry only when appropriate.

---

# Comments

Comments should explain *why*, not *what*.

Prefer expressive code over excessive comments.

---

# Testing

Every public module should include tests.

Focus on:

* Unit Tests
* Integration Tests

Critical workflows should have end-to-end tests.

---

# Git

Use Conventional Commits.

Examples:

feat(memory): implement retrieval service

fix(api): validate JWT

docs: update architecture

refactor(agent): simplify planner

---

# Pull Requests

Every PR should:

* Compile successfully
* Pass tests
* Update documentation if required

---

# Dependencies

Before adding a dependency, ask:

* Is it necessary?
* Is it maintained?
* Is it secure?
* Can we implement this ourselves?

Minimize unnecessary dependencies.

---

# Security

Never commit:

* Secrets
* API Keys
* Tokens
* Passwords

Use environment variables.

---

# Performance

Optimize only after measuring.

Avoid premature optimization.

---

# Documentation

Major architectural changes require documentation updates.

Code and documentation should evolve together.

---

# Success Criteria

A new contributor should be able to understand any module with minimal explanation.

Consistency is more valuable than individual preference.

---

# Version History

Version 1.0

Initial coding standards for the Sentinel project.

