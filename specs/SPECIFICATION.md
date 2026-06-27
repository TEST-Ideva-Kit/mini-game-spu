# Feature Specification: Mini Game - SPU

**Feature Branch**: `001-project-name-mini`
**Created**: 2026-06-27
**Status**: Draft
**Input**: User description: "Project name: Mini Game - SPU"

## User Scenarios & Testing *(mandatory)*

<!--
  IMPORTANT: User stories should be PRIORITIZED as user journeys ordered by importance.
  Each user story/journey must be INDEPENDENTLY TESTABLE - meaning if you implement just ONE of them,
  you should still have a viable MVP (Minimum Viable Product) that delivers value.

  Assign priorities (P1, P2, P3, etc.) to each story, where P1 is the most critical.
  Think of each story as a standalone slice of functionality that can be:
  - Developed independently
  - Tested independently
  - Deployed independently
  - Demonstrated to users independently
-->

### User Story 1 - Core Scoring and Combo Mechanic (Priority: P1)

A player engages with the game by hitting notes in time with the music. Successfully hitting notes increases their score and maintains a combo multiplier. Missing a note breaks the combo. The Turntable Bee character's 'Overdrive' ability activates after a certain combo threshold, significantly increasing score for perfect hits during its duration.

**Why this priority**: This is the fundamental gameplay loop and the primary way players interact with and are scored in the game.

**Independent Test**: A player can play a song from start to finish, and the final score accurately reflects the notes hit, misses, and combo multipliers, demonstrating the core scoring system.

**Acceptance Scenarios**:

1.  **Given** a song is playing, **When** the player hits a note with 'Perfect' timing, **Then** their score increases by the base note value multiplied by the current combo multiplier, and the combo counter increments.
2.  **Given** a song is playing, **When** the player hits a note with 'Good' timing, **Then** their score increases by a reduced value, and the combo counter increments.
3.  **Given** a song is playing, **When** the player misses a note, **Then** the combo counter resets to zero, and no score is awarded for that note.
4.  **Given** the player is using the Turntable Bee character and their combo reaches 50, **When** they hit a 'Perfect' note, **Then** the 'Overdrive' ability is activated, indicated visually, and subsequent 'Perfect' note scores are further amplified.

---

### User Story 2 - Combo Protection with Shields (Priority: P2)

The Aqua Girl character provides a defensive layer. When the player makes an error (misses a note) and has shields available, one shield is consumed, and the note is treated as a 'Good' instead of a 'Miss'. This preserves the player's combo and allows them to recover from minor mistakes.

**Why this priority**: This mechanic lowers the barrier to entry for new players by forgiving small mistakes, making the game more accessible and enjoyable for a wider audience.

**Independent Test**: A player can intentionally miss a note while Aqua Girl's shields are active, observe a shield being consumed, and confirm that their combo is maintained.

**Acceptance Scenarios**:

1.  **Given** the player is using Aqua Girl and has shields remaining, **When** they miss a note, **Then** one shield is consumed, the note is registered as 'Good', and the combo is maintained.
2.  **Given** the player is using Aqua Girl and has no shields remaining, **When** they miss a note, **Then** the combo is broken as normal, and no shield is consumed.
3.  **Given** the player starts a song with Aqua Girl, **When** no notes are missed, **Then** shields are not consumed.

---

### User Story 3 - Fever Mode and Hit Window Expansion (Priority: P3)

The DJ Puff character features a 'Fever Bar' that fills as the player achieves 'Perfect' hits. Once full, the player can activate 'Fever Mode', which temporarily expands the timing window for hitting notes, making it easier to achieve 'Perfect' hits and sustain combos during this period.

**Why this priority**: This adds a strategic layer and a 'risk-reward' element, offering a temporary advantage that players can utilize to maximize their score or recover from difficult sections.

**Independent Test**: A player can successfully achieve 'Perfect' hits to fill the Fever Bar, activate Fever Mode, and then observe that the timing window for hitting subsequent notes is demonstrably more forgiving.

**Acceptance Scenarios**:

1.  **Given** the player is using DJ Puff, **When** they hit notes with 'Perfect' timing, **Then** the 'Fever Bar' accumulates progress.
2.  **Given** the 'Fever Bar' is full, **When** the player presses the designated activation button, **Then** 'Fever Mode' is activated for a set duration, and the visual indicator for expanded hit windows appears.
3.  **Given** 'Fever Mode' is active, **When** the player hits a note within the expanded timing window, **Then** it is registered as a 'Perfect' hit.
4.  **Given** 'Fever Mode' has ended, **When** the player hits notes, **Then** the hit window returns to its standard size.

---

### Edge Cases

*   What happens if a combo-breaking event (e.g., a 'Miss' after shields deplete) occurs simultaneously with character ability activation (e.g., Overdrive or Fever mode)?
*   How does the game handle edge cases where multiple character abilities might overlap or conflict in their effects?
*   What is the behavior if a player triggers Fever Mode or Overdrive while shields are active and then misses a note? Does the shield still get consumed to preserve the combo, or does the ability take precedence?

## Requirements *(mandatory)*

<!--
  ACTION REQUIRED: The content in this section represents placeholders.
  Fill them out with the right functional requirements.
-->

### Functional Requirements

-   **FR-001**: System MUST allow players to interact with rhythm-based musical levels by hitting notes.
-   **FR-002**: System MUST track player performance based on timing accuracy (e.g., Perfect, Good, Miss).
-   **FR-003**: System MUST calculate and display player scores, incorporating combo multipliers.
-   **FR-004**: System MUST support distinct player characters, each with unique gameplay-altering abilities (score enhancement, combo protection, timing adjustment).
-   **FR-005**: System MUST load and interpret level data defined by a strict Beatmap JSON Schema.
-   **FR-006**: System MUST ensure data integrity for scores and leaderboard submissions using SHA-256 hashing.
-   **FR-007**: System MUST implement security measures based on STRIDE threat modeling principles.
-   **FR-008**: AI-generated code and assets MUST be subject to review and confirmation by human developers before integration.
-   **FR-009**: System MUST provide clear visual and auditory feedback for player actions and ability activations.
-   **FR-010**: System MUST synchronize gameplay timing with audio playback using an 'Audio-Clock Synchronizer' that avoids direct reliance on `Time.time` for critical calculations.
-   **FR-011**: [NEEDS CLARIFICATION: What is the precise score multiplier applied during Turntable Bee's 'Overdrive' state for 'Perfect' hits?]
-   **FR-012**: [NEEDS CLARIFICATION: How many shields does Aqua Girl begin with, and what is the exact visual or gameplay cue for losing the last shield?]
-   **FR-013**: [NEEDS CLARIFICATION: What is the exact duration of DJ Puff's 'Fever Mode' and the specific percentage by which the hit window is expanded?]

### Key Entities *(include if feature involves data)*

-   **Beatmap**: Defines a musical level, including song details, BPM, note count, and a sequence of notes with their timing and lane. Conforms to the Beatmap JSON Schema.
-   **Player**: The user controlling the gameplay.
-   **Character**: An entity that a player selects, granting them specific abilities.
-   **Ability**: A modifier applied to gameplay mechanics, tied to a specific Character. Examples include Score Enhancement, Combo Protection, and Hit Window Adjustment.
-   **Note**: An individual rhythm element within a Beatmap, requiring player interaction at a specific beat and lane.

## Success Criteria *(mandatory)*

<!--
  ACTION REQUIRED: Define measurable success criteria.
  These must be technology-agnostic and measurable.
-->

### Measurable Outcomes

-   **SC-001**: Players can successfully complete a song, achieving scores that accurately reflect their note-hitting accuracy and combo maintenance.
-   **SC-002**: Character abilities (e.g., score boosts, combo preservation, timing adjustments) demonstrably alter gameplay as described in their respective scenarios and are correctly applied.
-   **SC-003**: The game correctly parses and utilizes level data from Beatmap JSON files, presenting notes and timing information accurately.
-   **SC-004**: All submitted scores and leaderboard data are protected against tampering, verified by SHA-256 hashing.
-   **SC-005**: Gameplay timing remains perfectly synchronized with audio playback, with no discernible audio drift over the duration of a song.
-   **SC-006**: AI-assisted development tasks (e.g., boilerplate code generation) are integrated efficiently and confirmed by human developers, as per project policy.
-   **SC-007**: Player feedback indicates clear understanding and perceived fairness of the scoring, combo, and character ability systems.

---

## Existing Project Context

The following documents have already been generated for this project.
Use them to ensure consistency and avoid contradicting prior decisions:

### CONSTITUTION.md


# Mini Game - SPU Constitution

## Core Principles

### I. Spec-Driven Development
All development will be guided by formal specifications (PRD, Spec Kit artifacts). Architecture, features, and implementation details must be documented in `SPECIFICATION.md`, `PLAN.md`, `TASKS.md`, and `IMPLEMENTATION.md` before coding begins. This ensures alignment and traceability.

### II. Robust Technical Architecture

Systems will be built with a focus on reliable synchronization and deployment. Key architectural components like the Audio-Clock Synchronizer must adhere to strict system rules (e.g., avoiding `Time.time` for critical timing). Deployment pipelines (e.g., Unity WebGL via Railway/Vercel) must be automated and verifiable.

### III. Secure &amp; Auditable Data

All data, especially user-generated content like beatmaps and scores, must be secured and auditable. Implement robust security measures such as SHA-256 hashing for data integrity and STRIDE threat modeling to protect against common vulnerabilities. Beatmap data must conform to a strict JSON Schema.

### IV. Multi-Agent AI Collaboration

Leverage AI agents for structured development tasks, code generation, and routing. Adhere to defined AI policies (e.g., `Promptzone_config`) for AI tiering, code merging, and autonomy levels, ensuring predictable and controllable AI-assisted development.

### V. Structured Gameplay Mechanics &amp; Assets

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
**Ratification Date:** 2026-06-27
**Last Amended Date:** 2026-06-27
### PRD.md

🎮 GAME SPECIFICATION & PROJECT
PROPOSAL

PROJECT NAME: Music Mania (2026 Modernized Edition) STUDIO POSITIONING: Enterprise
AI-Assisted
Co-Production
(Digital Media Faculty Pilot)
FRAMEWORK: Spec-Driven Development (SDD) via Promptzone Architectural Command Center
🏗 มิติ ที่ 1: สถาปัตยกรรม ระบบ หลัง บ้าน และ การ วาง ระบบ (Technical Architecture)
เพื่อ ความ เป็น สากล และ สามารถ แสดง ผล บน Promptzone Website ได้ ทันที ผ่านแท็ก ตัว เกม จะ ถูกสร้าง ขึ้น ด้วย สถาปัตยกรรม ดังนี้ :
1. Audio-Clock Synchronizer (Conductor.cs)
● กฎ เหล็ก เชิง ระบบ (System Rule): ห้าม ใช้ Time.time ใน การ คํานวณ การ เคลื่อนที่ ของ โน้ต ดนตรี โดยเด็ดขาด
● ตรรกะ แกน หลัก : ตัว เกม ต้อง คํานวณ ตําแหน่ง จังหวะ ผ่าน ระบบ เวลา Audio Hardware ของ Unity
โดย ใช้ สูตร :
secPerBeat = (60.0f / bpm)
songPosition = (AudioSettings.dspTime - dspSongTime) - startDelay
songPositionInBeats = (songPosition / secPerBeat)
● Quality Gate: ระบบ Parity Gate ของ Promptzone จะ ทํา การ รัน สค ริปต์ทดสอบ (Unit Test) บน Local Machine ของ นักศึกษา เพื่อตรวจ จับ อัตรา การ หลุด จังหวะ (Audio Drift) ก่อน อนุญาต ให้ Commit
2. Sandbox Build & Deployment Specs
● Build Target: Unity 6 WebGL (Headless / Batchmode Build via Railway)
● Deployment Pipeline: เมื่อ Conductor Agent ส่ง สัญญาณ Socket จาก เครื่อง นักศึกษา แพลตฟอร์มจะ สั่ง รัน Docker Image บน Railway เพื่อ คอมไพล์โปรเจกต์เป็นไฟล์ Static Web แล้วผลัก ขึ้น Vercel เพื่อ นําลิงก์ มาฝัง บน Web UI ทันที
🎭 มิติ ที่ 2: เมท ริก ซ์การ ออก แบบ ตัว ละคร และ ระบบสกิล (Character Design & Ability Specs)
อ้างอิง จาก คลัง ตัว ละคร ดั้งเดิม ในไฟล์ Monomania_Musicmania_noDS.pdf เรา จะ แปลง ลักษณะ ทาง ศิลปะ (Artistic Persona) ให้ กลาย เป็น ตรรกะ เชิง ระบบ (Game Mechanics) เพื่อให้ AI และ นักศึกษา นํา ไป เขียน โปรแกรม ร่วม กับ ระบบ Event-Driven System ได้ อย่าง แม่นยํา :
[BaseCharacter]
│
┌───────────────────────┼───────────────────────┐
▼                       ▼                       ▼
(Turntable Bee)          (Aqua Girl)             (DJ Puff)
[Score Enhancer]       [Shield & Recovery]     [Mechanic Tweaker]

1. Turntable Bee ( ตัว ต่อ สี เหลือง สวม หู ฟัง ดี เจ )
● สาย งาน : Score Enhancer ( สาย เน้น ทํา คะแนน ระดับ สูง )
● คํา อธิบาย พฤติกรรมสกิล (C# Data Structure):
○ ดัก จับ สถานะ ผ่าน อิน เทอร์เฟซ ICharacterAbility
○ เมื่อ ตัวแปร currentCombo >= 50 ระบบ จะ เปิด ใช้ งาน สถานะ Overdrive
○ สูตร คํานวณ คะแนน : ใน ขณะ ที่ สถานะ นี้ ทํา งาน โน้ต ที่ กด ได้ Perfect จะ ถูก คํานวณ ใหม่ เป็น :
NoteScore = 300 × 1.10 × (ComboMultiplier)
● Animation State Triggers: สั่ง งาน ผ่าน สค ริปต์ CharacterAnimationController ให้ เปลี่ยน สถานะ ใน Animator ไป ที่ ท ริกเกอร์ OnOverdriveActive เพื่อ เปิด เอฟ เฟกต์แสง ไฟ ดิสโก้รอบ ตัวละคร
2. Aqua Girl ( ตัว ละคร ธาตุ นํ้า สี ฟ้า สวม แว่นโกเกิ้ล )
● สาย งาน : Shield & Recovery ( สาย ป้องกัน สําหรับ ผู้ เล่น เริ่ม ต้น )
● คํา อธิบาย พฤติกรรมสกิล (C# Data Structure):
○ กําหนด ตัวแปร int shieldCount = 3 เมื่อ เริ่ม ต้น เพลง
○ เมื่อ ระบบ PlayerInput.cs ส่ง สัญญาณ Event onNoteMiss ให้ ทํา การ ดัก จับ (Intercept) สัญญาณ ก่อน คลาส คํานวณ คะแนน หลัก จะ รับรู้
○ เงื่อนไข : หาก shieldCount > 0 ให้ ทํา ลด ค่า shieldCount-- และ บังคับ ส่ง สถานะ หลอก (Fake State) เป็น Good แทน เพื่อรักษา เส้น สะสม Combo ของ ผู้ เล่น ไม่ ให้ กลาย เป็น 0
● Animation State Triggers: เล่น อ นิ เม ชัน ท่า OnGuardShield พร้อม ทํา เอฟ เฟกต์ฟอง สบู่ แตก กระจาย บน จอ
3. DJ Puff ( ตัว ละคร แปด แขน สี ส้ม สวม หน้ากาก แก๊ส ลําโพง )
● สาย งาน : Mechanic Tweaker ( สาย ปรับ แต่ง โครงสร้าง เกม เชิง เวลา )
● คํา อธิบาย พฤติกรรมสกิล (C# Data Structure):
○ มี หลอด สะสม ค่า พลังงาน FeverBar ( รับ ค่า เพิ่ม ขึ้น +1% ทุก ครั้ง ที่ กด จังหวะ Perfect)
○ เมื่อ หลอด พลังงาน เต็ม ผู้ เล่น สามารถ กด ปุ่ม Spacebar เพื่อ เปิด ใช้ งาน Fever Mode เป็น เวลา 5 วินาที
○ พฤติกรรม เชิง ระบบ : ระบบ จะ เปลี่ยน ค่าตัว แปรก รอบ เวลา การก ด จังหวะ (Hit Window Offset) ใน สค ริปต์ PlayerInput.cs จาก เดิม 0.1s ขยาย เป็น 0.115s (+15%) ชั่วคราว เพื่อ เพิ่ม โอกาส การก ด Perfect ใน จังหวะ เพลงเร็ว
● Animation State Triggers: ท ริก เก อร์อ นิ เม ชัน ท่า FeverDance และ เปลี่ยน แถบ สี ของ ลู่ กด โน้ต ทั้ง 4 เลน เป็น สี ทอง สว่าง
🗺 มิติ ที่ 3: ระบบ ด่าน และ กรอบ ความ ปลอดภัย (Level Design & Security Rules)
ตัว เกม จะ ประกอบ ไป ด้วย 5 โซ น ตาม ภาพ แผนที่ โลก ต้นฉบับ ซึ่ง ระบบ Beatmap Recorder จะ ต้อง แปลง ผลลัพธ์ ออก มา เป็น โครงสร้าง ข้อมูล มาตรฐาน เพื่อ ส่ง ขึ้น ไป โฮสต์และ รี วิว บน หน้าเว็บ คอม มูนิตี้ของ Promptzone:
1. โครงสร้าง ไฟล์ข้อมูล ด่าน (Beatmap JSON Schema)
AI Worker และ สค ริปต์เขียน ไฟล์จะ ต้อง ส่ง ออก ข้อมูล สอดคล้อง ตาม โครงสร้าง นี้ เท่านั้น เพื่อ ผ่าน ด่าน Security Gate ( ตรวจ สอบ การ แฝง โค้ดอันตราย หรือ System Path หลุด รอด ):
{
"beatmapId": "musicmania_zone1_pub",
"songName": "To Be Star",
"bpm": 128.0,
"noteCount": 420,
"levelZone": "PinkPubDistrict",
"notes": [
{ "beat": 4.0, "lane": 0 },
{ "beat": 4.5, "lane": 2 },
{ "beat": 5.0, "lane": 1 },
{ "beat": 5.0, "lane": 3 }
]
}
2. Shift-Left Security & STRIDE Mapping
● Spoofing & Tampering Protection: สค ริ ปต์ระบบ คะแนน และ การ ส่ง ข้อมูล Leaderboard ไป ยัง หน้าเว็บ จะ ต้อง วิ่ง ผ่าน กลไก การ เข้ารหัส Hash แบบ SHA-256 ผูก กับ รหัส นักศึกษา เพื่อป้องกัน ไม่ ให้ นักศึกษา แอบ ใช้ วิธี ส่ง ข้อมูล คะแนน ปลอม เข้า API เว็บก ลาง
🤖 มิติ ที่ 4: พิมพ์เขียว สั่ง การ ระบบ Multi-Agent AI (Promptzone Configuration)
เพื่อให้ นักศึกษา ทํา งาน แบบ Strategic Architect (Agent Boss) ควบคุม AI ไม่ ให้ เกิด Spaghetti Code ให้ เรา เขียน ค่า กําหนด (Configurations) นี้ ตั้ง ไว้ บน แพลตฟอร์ม:
promptzone_config:
ai_tier_policy:
cloud_platform_ai: "Stateless (Haiku-class) for Task breakdown & API routing"
local_agent_ai: "Stateful (Claude-class) inside student machine via Conductor daemon"
code_merge_policy:
engine: "Hash-Anchored Edits Enabled"
conflict_resolution: "Identify stable-line anchors before merging player/score/conductor branches"
autonomy_dial:
core_logic_scripts: "Suggest-Only (Requires student review & emoji confirmation)"
ui_vfx_assets: "Semi-Autonomous (AI writes boilerplate, student tweaks parameters)"

หน้าที่ บน บอร์ด งาน (Kanban Assignment Framework):
● Agent 1 (Orchestrator): ส แกน ส เปก ตัว ละคร 3 ตัว ข้าง ต้น แล้ว ทํา การ แตก งาน สร้าง ไฟล์คลา ส หลัก เช่น ICharacterAbility.cs, CharacterBase.cs ลง ลู่ บอร์ด งาน ของ โปรแกรม เมอร์
● Agent 2 (VFX/UI Worker): รับหน้า ส เปก เรื่อง ของ เอฟ เฟกต์ฟอง สบู่ เพื่อ ไป เจน คําสั่ง ระเบิดพาร์ทิเคิล (Particle System) ให้ ฝั่ง Technical Artist นํา ไป สวม ใน Unity เอน จิ น ทันที

### README.md

# Project specs

This folder holds **Spec Kit** artifacts for this project (same idea as [GitHub Spec Kit](https://github.github.io/spec-kit/)).

| File | Workflow step |
|------|----------------|
| `CONSTITUTION.md` | Principles and constraints |
| `SPECIFICATION.md` | What to build |
| `PLAN.md` | Architecture and delivery |
| `TASKS.md` | Engineering task list |
| `IMPLEMENTATION.md` | Implementation outline |

Use the **Spec Kit workflow** in the workspace to generate or edit these files. Optional notes and requirements can live in other project documents.