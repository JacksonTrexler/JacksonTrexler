# Agentic Security Workflows

This document captures a practical framework for designing and reviewing agentic workflows with security as a first-class concern.

## Goals

- Keep autonomous or semi-autonomous agents aligned with policy and business intent
- Reduce the blast radius of prompt injection, unsafe tool use, and over-privileged automation
- Make security decisions visible and reviewable by humans

## Core Principles

### 1. Least privilege

Every agent should receive only the permissions needed for the task. Avoid broad repository, cloud, or shell access unless absolutely required.

### 2. Human approval for high-impact actions

Actions that create, modify, delete, deploy, or expose sensitive data should require explicit approval or a structured review checkpoint.

### 3. Explicit task boundaries

Define the allowed scope, expected inputs, and prohibited operations in clear terms. Treat the instructions as policy, not just guidance.

### 4. Observability and auditability

Capture tool invocations, decisions, and reasoning checkpoints so security reviews can reconstruct what happened.

### 5. Defense in depth

Use layered controls such as input validation, prompt sanitization, policy enforcement, environment isolation, and outbound restrictions.

## Recommended Workflow

1. Define the mission and risk profile.
2. Classify the task as read-only, write-capable, or privileged.
3. Restrict tools and environment bindings to the minimum required.
4. Validate inputs and outputs before acting on them.
5. Require confirmation for irreversible or sensitive operations.
6. Log actions and attach context for later review.
7. Reassess after failures, anomalies, or privilege changes.

## Security Controls Checklist

- Confirm the agent cannot access secrets outside the approved environment.
- Block untrusted content from controlling privileged workflows.
- Validate external data before branching or executing commands.
- Use allowlists for tools, commands, network destinations, and file paths.
- Escalate when tasks exceed policy thresholds or confidence limits.
- Maintain a clear rollback strategy for critical operations.

## Example Governance Pattern

- Normal operations: agent may read files and propose actions
- Medium risk: human review required before execution
- High risk: human approval + second-party confirmation + audit log preserved

## Operational Notes

Security is not just a prompt issue. It is a system design problem involving identity, execution boundaries, monitoring, and governance. Agentic systems are safer when the policy model is explicit and the execution model is constrained.

## Next Steps

- Add a repository-level task classification policy.
- Document which tools are allowlisted and under what conditions.
- Define a standard approval workflow for destructive actions.
- Add a review checklist for agent-generated pull requests, commits, or deployment steps.
