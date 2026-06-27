
# Mini Game - SPU Constitution

## Core Principles

### I. Spec-Driven Development
All development will be guided by formal specifications (PRD, Spec Kit artifacts). Architecture, features, and implementation details must be documented in SPECIFICATION.md, PLAN.md, TASKS.md, and IMPLEMENTATION.md before coding begins. This ensures alignment and traceability.

### II. Robust Technical Architecture
Systems will be built with a focus on reliable synchronization and deployment. Key architectural components like the Audio-Clock Synchronizer must adhere to strict system rules (e.g., avoiding Time.time for critical timing). Deployment pipelines (e.g., Unity WebGL via Railway/Vercel) must be automated and verifiable.

### III. Secure &amp; Auditable Data
All data, especially user-generated content like beatmaps and scores, must be secured and auditable. Implement robust security measures such as SHA-256 hashing for data integrity and STRIDE threat modeling to protect against common vulnerabilities. Beatmap data must conform to a strict JSON Schema.

### IV. Multi-Agent AI Collaboration
Leverage AI agents for structured development tasks, code generation, and routing. Adhere to defined AI policies (e.g., Promptzone_config) for AI tiering, code merging, and autonomy levels, ensuring predictable and controllable AI-assisted development.

### V. Structured Gameplay Mechanics &amp; Assets
Gameplay mechanics and character abilities will be defined using clear, systemic data structures (e.g., C# Data Structures, ICharacterAbility interface). Animations will be triggered via defined controllers. Visual assets and effects must be well-defined and integrated systematically.

## Security &amp; Compliance

- Adherence to the defined Beatmap JSON Schema is mandatory for all level data.
- All data transmissions for leaderboards and scores must pass through SHA-256 hashing and student ID verification to prevent tampering.
- Code merging will follow "Hash-Anchored Edits" with clear conflict resolution strategies.
- AI autonomy levels will be strictly managed as per Promptzone_config, with core logic requiring student review and confirmation.

## Spec Kit Workflow &amp; AI Integration

- The project will utilize the Spec Kit workflow, with CONSTITUTION.md, SPECIFICATION.md, PLAN.md, TASKS.md, and IMPLEMENTATION.md being central artifacts.
- AI agents (Orchestrator, VFX/UI Worker) will be used to break down tasks from specifications and generate boilerplate code/assets, which will then be reviewed and refined by human developers.
- AI-driven code generation must be suggested and confirmed by developers.

## Governance Rules

- This Constitution supersedes all other practices within the project.
- Amendments to this Constitution require formal documentation, approval, and a clear migration plan for affected artifacts and code.
- All code reviews and PRs must verify compliance with these principles and constraints.
- Complexity in implementation must be clearly justified.
- Runtime development guidance should be referenced from the README.md within the specs directory.

**Version:** 1.0.0 | **Ratified:** 2026-06-27 | **Last Amended:** 2026-06-27
``````html


# Mini Game - SPU Project Constitution

**Version:** 1.0.0
**Ratification Date:** 2026-06-27
**Last Amended Date:** 2026-06-27

## I. Spec-Driven Development

All development will be guided by formal specifications (PRD, Spec Kit artifacts). Architecture, features, and implementation details must be documented in `SPECIFICATION.md`, `PLAN.md`, `TASKS.md`, and `IMPLEMENTATION.md` before coding begins. This ensures alignment and traceability.

## II. Robust Technical Architecture

Systems will be built with a focus on reliable synchronization and deployment. Key architectural components like the Audio-Clock Synchronizer must adhere to strict system rules (e.g., avoiding `Time.time` for critical timing). Deployment pipelines (e.g., Unity WebGL via Railway/Vercel) must be automated and verifiable.

## III. Secure &amp; Auditable Data

All data, especially user-generated content like beatmaps and scores, must be secured and auditable. Implement robust security measures such as SHA-256 hashing for data integrity and STRIDE threat modeling to protect against common vulnerabilities. Beatmap data must conform to a strict JSON Schema.

## IV. Multi-Agent AI Collaboration

Leverage AI agents for structured development tasks, code generation, and routing. Adhere to defined AI policies (e.g., `Promptzone_config`) for AI tiering, code merging, and autonomy levels, ensuring predictable and controllable AI-assisted development.

## V. Structured Gameplay Mechanics &amp; Assets

Gameplay mechanics and character abilities will be defined using clear, systemic data structures (e.g., C# Data Structures, `ICharacterAbility` interface). Animations will be triggered via defined controllers. Visual assets and effects must be well-defined and integrated systematically.

## Security &amp; Compliance

- Adherence to the defined Beatmap JSON Schema is mandatory for all level data.
- All data transmissions for leaderboards and scores must pass through SHA-256 hashing and student ID verification to prevent tampering.
- Code merging will follow "Hash-Anchored Edits" with clear conflict resolution strategies.
- AI autonomy levels will be strictly managed as per `Promptzone_config`, with core logic requiring student review and confirmation.

## Spec Kit Workflow &amp; AI Integration

- The project will utilize the Spec Kit workflow, with `CONSTITUTION.md`, `SPECIFICATION.md`, `PLAN.md`, `TASKS.md`, and `IMPLEMENTATION.md` being central artifacts.
- AI agents (Orchestrator, VFX/UI Worker) will be used to break down tasks from specifications and generate boilerplate code/assets, which will then be reviewed and refined by human developers.
- AI-driven code generation must be suggested and confirmed by developers.

## Governance Rules

- This Constitution supersedes all other practices within the project.
- Amendments to this Constitution require formal documentation, approval, and a clear migration plan for affected artifacts and code.
- All code reviews and PRs must verify compliance with these principles and constraints.
- Complexity in implementation must be clearly justified.
- Runtime development guidance should be referenced from the `README.md` within the `specs` directory.

**Version:** 1.0.0
```