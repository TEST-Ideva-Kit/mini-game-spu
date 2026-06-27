# Implementation Plan: Mini Game - SPU

**Branch**: `001-project-name-mini` | **Date**: 2026-06-27 | **Spec**: `specs/001-project-name-mini/spec.md`
**Input**: Feature specification from `/specs/001-project-name-mini/spec.md`

## Summary

This plan outlines the technical implementation for the "Mini Game - SPU" feature, focusing on a spec-driven development approach within the Unity game engine. The core gameplay loop will be established, featuring a robust scoring system, combo mechanics, and distinct character abilities (Turntable Bee's score enhancement, Aqua Girl's combo protection, and DJ Puff's hit window expansion). The implementation will prioritize reliable synchronization via an Audio-Clock Synchronizer, secure data handling with SHA-256 hashing, adherence to a Beatmap JSON Schema, and integration with multi-agent AI collaboration policies for code generation and deployment via Unity WebGL, Railway, and Vercel.

## Technical Context

**Language/Version**: Unity (C#)
**Primary Dependencies**: Unity Engine, `Conductor.cs`, `PlayerInput.cs`, `CharacterAnimationController`, `ICharacterAbility.cs` interface, Beatmap JSON Schema parser.
**Storage**: JSON files for Beatmaps. Backend integration (TBD) for scores and leaderboards with SHA-256 hashing.
**Testing**: Unity Unit Tests, System Parity Gate for Audio Drift.
**Target Platform**: Unity WebGL (Headless / Batchmode Build via Railway)
**Project Type**: Game (Rhythm Game)
**Performance Goals**: 60 fps, minimal audio drift (< 0.1s deviation), low latency input processing.
**Constraints**:
*   Strict system rules for timing (avoid `Time.time` for critical calculations).
*   Beatmap data must conform to a strict JSON Schema.
*   SHA-256 hashing for score integrity.
*   STRIDE threat modeling principles for security.
*   AI autonomy levels managed per `Promptzone_config`.
**Scale/Scope**: Implement 3 distinct character abilities across potentially 5 game zones.

## Constitution Check# Implementation Plan: Mini Game - SPU

**Branch**: `001-project-name-mini` | **Date**: 2026-06-27 | **Spec**: /specs/001-project-name-mini/spec.md

**Note**: This template is filled in by the `/speckit.plan` command. See `.specify/templates/plan-template.md` for the execution workflow.

## Summary

This plan details the technical implementation for the "Mini Game - SPU" feature, a rhythm game developed in Unity with a focus on Spec-Driven Development, robust architecture, secure data handling, and AI collaboration. The game will feature distinct player characters with unique abilities that modify core gameplay mechanics like scoring, combo preservation, and hit windows. Development will adhere to the project's constitution, leveraging Unity's WebGL capabilities for deployment and implementing an Audio-Clock Synchronizer to avoid direct reliance on `Time.time` for critical timing.

## Technical Context

**Language/Version**: C# (Unity Engine - latest stable version assumed)
**Primary Dependencies**: Unity Engine, Unity Test Framework (or equivalent for unit testing audio sync), JSON parsing library (e.g., Unity's built-in JsonUtility or Newtonsoft.Json).
**Storage**: Beatmap data will be loaded from JSON files conforming to the specified schema. Player scores and integrity checks will be handled according to the constitution, with potential for future backend integration.
**Testing**: Unit tests for core game logic, character abilities, and critically, the Audio-Clock Synchronizer for audio drift. Integration tests for beatmap loading and playback.
**Target Platform**: Unity WebGL.
**Project Type**: Game.
**Performance Goals**: Smooth 60 FPS gameplay, minimal audio drift (< 10ms per minute or as defined by Unity best practices for audio sync).
**Constraints**:
*   Strict adherence to the Audio-Clock Synchronizer pattern, avoiding `Time.time` for note timing calculations.
*   Implementation of SHA-256 hashing for score integrity.
*   Full compliance with the Beatmap JSON Schema.
*   AI-assisted code generation and asset integration as per `promptzone_config`.
**Scale/Scope**: Core rhythm game mechanics, 3 distinct characters with unique abilities, beatmap loading and playback, basic scoring and combo system.

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

*   **I. Spec-Driven Development**: This plan is directly derived from `SPECIFICATION.md` and `PRD.md`. All subsequent development phases will follow the Spec Kit workflow. (Pass)
*   **II. Robust Technical Architecture**: The plan incorporates the Audio-Clock Synchronizer pattern to ensure reliable synchronization, avoiding `Time.time`. Unity WebGL and a conceptual deployment pipeline align with the architecture requirements. (Pass)
*   **III. Secure & Auditable Data**: The plan includes implementing SHA-256 hashing for score integrity and strict adherence to the Beatmap JSON Schema, as mandated. STRIDE threat modeling will be considered during implementation. (Pass)
*   **IV. Multi-Agent AI Collaboration**: The plan acknowledges AI roles (Orchestrator, VFX/UI Worker) for generating boilerplate code and assets, with human review as per `promptzone_config`. (Pass)
*   **V. Structured Gameplay Mechanics & Assets**: Character abilities are planned as systemic data structures (`ICharacterAbility`) and integrated via animation triggers, aligning with the principle of structured mechanics. (Pass)

## Project Structure

### Documentation (this feature)

```text
specs/001-project-name-mini/
├── plan.md              # This file
├── spec.md              # Feature specification
├── research.md          # Phase 0 output (TBD)
├── data-model.md        # Phase 1 output (TBD)
├── quickstart.md        # Phase 1 output (TBD)
└── checklists/
    └── requirements.md  # Existing requirements checklist
```

### Source Code (repository root)

```text
# Unity Project Structure
Assets/
├── Scenes/             # Game scenes (e.g., MainMenu, Gameplay)
│   └── Gameplay.unity
├── Scripts/            # All C# scripts
│   ├── Core/           # Core game systems (AudioClockSync, ScoreManager, ComboManager)
│   │   ├── AudioClockSynchronizer.cs
│   │   ├── ScoreManager.cs
│   │   └── ComboManager.cs
│   ├── Characters/     # Character-specific logic and data
│   │   ├── ICharacterAbility.cs
│   │   ├── CharacterBase.cs
│   │   ├── TurntableBee.cs
│   │   ├── AquaGirl.cs
│   │   └── DJPuff.cs
│   ├── Gameplay/       # Note spawning, hit detection, UI elements
│   │   ├── NoteSpawner.cs
│   │   ├── HitDetector.cs
│   │   ├── BeatmapLoader.cs
│   │   └── GameplayUI.cs
│   ├── Animation/      # Animation controller scripts
│   │   └── CharacterAnimationController.cs
│   └── Utilities/      # General helper scripts (e.g., Hashing)
│       └── SHA256Hasher.cs
├── Prefabs/            # Reusable game objects (Notes, characters, effects)
├── ScriptableObjects/  # For character data, beatmap data (if not fully JSON)
├── Audio/              # Sound effects and music
├── Art/                # Visual assets
└── ...                 # Other Unity project folders (e.g., Plugins, Resources)
```

**Structure Decision**: A standard Unity project structure is adopted, with game logic organized into `Assets/Scripts/` subfolders based on functionality (Core, Characters, Gameplay, Animation, Utilities). This allows for clear separation of concerns and aligns with typical Unity development patterns.

## Complexity Tracking

> **Fill ONLY if Constitution Check has violations that must be justified**

| Violation | Why Needed | Simpler Alternative Rejected Because |
|-----------|------------|-------------------------------------|
| N/A | N/A | N/A |

## Phased Delivery Plan

### Phase 0: Research & Setup (Approx. 1-2 days)

*   **Objective**: Understand Unity's audio timing mechanisms, set up the Unity project, and establish the basic project structure.
*   **Tasks**:
    *   Research Unity's `AudioSettings.dspTime` and best practices for precise audio synchronization.
    *   Set up a new Unity project, configure it for WebGL build.
    *   Create the initial folder structure within `Assets/Scripts/` as defined above.
    *   Research and select a suitable JSON parsing library for Unity if `JsonUtility` is insufficient for the Beatmap Schema.
*   **Deliverables**: Project structure, documented research on audio sync.
*   **Risks**: Difficulty in achieving precise audio synchronization without `Time.time`.

### Phase 1: Core Gameplay Mechanics (Approx. 3-5 days)

*   **Objective**: Implement the fundamental rhythm game loop: note spawning, hit detection, basic scoring, and combo management.
*   **Tasks**:
    *   Implement `AudioClockSynchronizer.cs` to manage song playback and beat timing.
    *   Implement `BeatmapLoader.cs` to parse Beatmap JSON files.
    *   Implement `NoteSpawner.cs` to instantiate notes based on beatmap data.
    *   Implement `HitDetector.cs` for player input and timing accuracy detection (Perfect, Good, Miss).
    *   Implement `ScoreManager.cs` and `ComboManager.cs` to track scores and combos.
    *   Create basic note prefabs.
*   **Deliverables**: Playable core loop with notes appearing and being hit, score and combo updates.
*   **Risks**: Ensuring the `AudioClockSynchronizer` is robust and accurate; potential for off-sync notes if timing calculations are incorrect.

### Phase 2: Character Abilities Implementation (Approx. 5-7 days)

*   **Objective**: Implement the character system and each character's unique abilities.
*   **Tasks**:
    *   Define `ICharacterAbility.cs` interface.
    *   Implement `CharacterBase.cs` abstract class.
    *   Implement `TurntableBee.cs`: Overdrive score enhancement logic.
    *   Implement `AquaGirl.cs`: Shield and combo preservation logic.
    *   Implement `DJPuff.cs`: Fever Bar, Fever Mode activation, and hit window expansion logic.
    *   Integrate `CharacterAnimationController.cs` to trigger relevant animations based on ability states.
    *   Create character prefabs and associate them with abilities.
*   **Deliverables**: Characters selectable, abilities active and affecting gameplay as per spec.
*   **Risks**: Complexity in managing state across multiple abilities and ensuring they interact correctly without conflicts.

### Phase 3: Data Integrity & Security (Approx. 2-3 days)

*   **Objective**: Ensure data integrity and adherence to security requirements.
*   **Tasks**:
    *   Implement `SHA256Hasher.cs` utility.
    *   Integrate SHA-256 hashing for score submissions (e.g., when a song is completed, generate a hash of score + student ID).
    *   Verify all Beatmap JSON parsing strictly adheres to the schema.
    *   Consider basic STRIDE threat modeling for data handling.
*   **Deliverables**: Functional score hashing mechanism, validated beatmap loading.
*   **Risks**: Overlooking edge cases in hashing or schema validation.

### Phase 4: AI Integration & Refinement (Approx. 3-5 days)

*   **Objective**: Integrate AI-generated components (if any) and refine UI/VFX.
*   **Tasks**:
    *   Use AI agents (Orchestrator, VFX/UI Worker) to generate boilerplate code or assets as per `promptzone_config`.
    *   Review and integrate AI-generated code, ensuring it aligns with project standards and the constitution.
    *   Implement visual and auditory feedback for character abilities (e.g., Overdrive effects, shield bubbles, Fever Mode indicators).
    *   Refine UI elements for score, combo, and ability status.
*   **Deliverables**: Integrated AI components, polished UI/VFX for abilities.
*   **Risks**: AI-generated code may require significant refactoring or may not meet quality standards.

### Phase 5: Testing & Deployment (Approx. 3-4 days)

*   **Objective**: Ensure quality through testing and prepare for deployment.
*   **Tasks**:
    *   Write comprehensive unit tests for `AudioClockSynchronizer`, character abilities, and score calculation.
    *   Perform integration tests for beatmap loading and playback.
    *   Conduct user acceptance testing (UAT) based on user stories.
    *   Configure Unity build settings for WebGL.
    *   Set up basic deployment pipeline (e.g., using Railway/Vercel as mentioned in PRD, though actual implementation is out of scope for this plan).
*   **Deliverables**: Verified game functionality, passing tests, WebGL build readiness.
*   **Risks**: Deployment issues specific to Unity WebGL or the chosen platform.

## Risks and Mitigation

*   **Audio Drift**:
    *   **Risk**: The `AudioClockSynchronizer` may not be perfectly accurate, leading to audio-visual desync.
    *   **Mitigation**: Rigorous research into Unity's audio timing APIs, extensive unit testing with clear thresholds, and potentially implementing a small buffer or correction mechanism if drift is detected.
*   **Character Ability Conflicts**:
    *   **Risk**: When multiple abilities are active or interact, unexpected behavior may occur.
    *   **Mitigation**: Design character abilities with clear state management and well-defined interaction rules. Use thorough unit and integration tests to cover ability interactions.
*   **AI-Generated Code Quality**:
    *   **Risk**: AI may produce suboptimal, incorrect, or hard-to-maintain code/assets.
    *   **Mitigation**: Adhere to `promptzone_config`'s "Suggest-Only" and review policies. Implement linters and static analysis tools where possible. Allocate sufficient time for human review and refactoring.
*   **WebGL Performance & Compatibility**:
    *   **Risk**: The game may not perform well or be compatible across all target browsers/devices.
    *   **Mitigation**: Profile performance regularly during development. Test builds on various platforms and browsers early in the WebGL development phase.
*   **Beatmap Data Validation**:
    *   **Risk**: Incorrectly formatted beatmap files could crash the game or cause gameplay errors.
    *   **Mitigation**: Implement robust error handling and validation in `BeatmapLoader.cs` to catch malformed JSON or schema deviations.
