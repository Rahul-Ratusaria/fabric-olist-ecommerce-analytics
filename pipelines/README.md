# Microsoft Fabric Pipeline

## Purpose

This folder documents the orchestration layer of the Microsoft Fabric project.

Instead of manually executing notebooks, a Fabric Pipeline automates the complete Medallion Architecture.

Execution Flow

Landing

↓

Profiling

↓

Bronze

↓

Silver

↓

Gold

The pipeline guarantees:

- sequential execution;
- dependency management;
- centralized monitoring;
- execution history;
- future scheduling support.

## Current Pipeline

The current orchestration contains five sequential notebook activities.

Activities

1. Landing
2. Bronze
3. Profiling
4. Silver
5. Gold

Each activity executes only after the previous activity succeeds.

Retry Policy

- Retries: 2
- Retry Interval: 30 seconds