# Microsoft Fabric Pipeline

## Purpose

This folder documents the orchestration layer of the Microsoft Fabric project.

Instead of manually executing notebooks, a Fabric Pipeline automates the complete Medallion Architecture.

Execution Flow

Landing

↓

Bronze

↓

Profiling

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

Status

In Progress