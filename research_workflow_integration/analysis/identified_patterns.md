# Identified Patterns in Workflow Integration Research

This document outlines key patterns and recurring themes identified during the initial data collection phase, analyzing `01_AI-RUN`, `02_AI-DOCS`, `03_SPECS`, and `.roomodes`. These patterns will inform the integration strategy.

## 1. Pattern: State-Driven Orchestration (`01_AI-RUN`)

*   **Description:** The `01_AI-RUN` workflow, particularly as orchestrated by `02_AutoPilot.md`, relies heavily on a central state file (`project_session_state.json`) to manage progress, track completed steps (`lastCompletedStep`), determine the current phase (`currentWorkflowPhase`), store document paths, and handle errors.
*   **Mechanism:** Decisions are made based on the contents of this JSON file. Each phase updates the state upon completion or error.
*   **Implication for Integration:** Integrating this level of granular, file-based state tracking directly into the existing `.roomodes` (which primarily use `.pheromone` for higher-level signals and a documentation registry) presents a significant architectural consideration. `.roomodes` orchestrators are generally stateless beyond reading `.pheromone` and their input task.

## 2. Pattern: Persona Adoption (`01_AI-RUN`)

*   **Description:** `02_AutoPilot.md` describes a mechanism where the orchestrating AI ("ProjectArchitect AI") adopts different personas (e.g., "MarketStrategist AI", "TechDocNavigator") defined within specific sub-prompts for each phase.
*   **Mechanism:** The persona is specified in the sub-prompt file, and the orchestrator temporarily assumes this role.
*   **Implication for Integration:** `.roomodes` agents have fixed personas defined by their `slug`, `name`, and `roleDefinition`. Implementing dynamic persona adoption as described would require a fundamental change to how modes operate or a new meta-orchestrator that can dynamically load/configure aspects of a worker mode based on a phase. Alternatively, specific phases from `01_AI-RUN` could be mapped to existing `.roomodes` agents whose fixed personas are already aligned.

## 3. Pattern: Template-to-Instance Document Generation (`01_AI-RUN`, `02_AI-DOCS`, `03_SPECS`)

*   **Description:** A core activity, especially in the "Specs & Docs" phase (guided by `07_Specs_Docs.md`), is the creation of project-specific documents by copying templates from `02_AI-DOCS` and `03_SPECS` and then populating these copies.
*   **Mechanism:** "Foolproof Template Copying" involves verifying template existence, checking for target file conflicts, copying, populating, and saving the new instance. Original templates are never modified.
*   **Implication for Integration:** Existing `.roomodes` worker agents (e.g., `spec-writer-feature-overview`, `architect-highlevel-module`) are designed to create output documents. The specific logic for *copying from a template first* and then populating needs to be explicitly added to their `customInstructions` if they are to fulfill these roles from `01_AI-RUN`.

## 4. Pattern: Hierarchical Document Structure and Inter-dependencies

*   **Description:** The `01_AI-RUN` workflow generates a series of documents where each phase builds upon the outputs of the previous ones (e.g., Idea -> Market Research -> Core Concept -> PRD -> Specs -> Tasks).
*   **Mechanism:** Outputs of one phase (e.g., `core_concept.md`) become critical inputs for the next (e.g., PRD generation). Paths to these documents are tracked (conceptually in `project_session_state.json`).
*   **Implication for Integration:** `.roomodes` orchestrators already manage dependencies to some extent by passing relevant document paths. This pattern aligns well but requires robust mechanisms for tracking and passing the correct, project-specific document paths between modes. The `documentation_registry` in `.pheromone` could serve a similar purpose to `project_session_state.json.documents`.

## 5. Pattern: Explicit MCP Tool Usage for Specific Tasks

*   **Description:** `01_AI-RUN/07_Specs_Docs.md` and `01_AI-RUN/08_Start_Building.md` prescribe the use of specific MCP tools (`context7`, `shadcn`, `@21st-dev/magic`, `github`, `firecrawl`) for particular tasks like documentation retrieval, UI component generation, and code management.
*   **Mechanism:** Sub-prompts for these phases would instruct the AI to use these tools with specific arguments.
*   **Implication for Integration:** While some `.roomodes` agents (e.g., `coder-test-driven`, `research-planner-strategic`) have general MCP usage permissions or mandates, the highly specific and prioritized usage of tools like `context7` (for library docs first) or `shadcn` (for UI components) needs to be explicitly incorporated into the `customInstructions` of relevant worker modes.

## 6. Pattern: Foundational Guidance Documents vs. Project Instances

*   **Description:** `02_AI-DOCS/Documentation/` contains files like `AI_Design_Agent_Optimization.md`. These are not templates to be copied per project but rather foundational knowledge or "core instructions" that the AI should internalize and apply when creating project-specific documents (like `design_conventions.md`).
*   **Mechanism:** The AI is expected to synthesize a "Structured Summary of UI/UX Principles" from these documents and use that summary to guide its work.
*   **Implication for Integration:** The `customInstructions` for relevant `.roomodes` agents (especially those dealing with design, UI/UX, or coding conventions) need to reflect this pattern of consulting and applying principles from these foundational documents when populating project-specific instances.

## 7. Pattern: Granular State Tracking and Error Handling (`01_AI-RUN`)

*   **Description:** `02_AutoPilot.md` defines a very granular state tracking system using `lastCompletedStep` (e.g., `idea_generation_file_saved`, `specsDocsPhase_copiedArchitectureTemplate`) and a structured `errorState` object.
*   **Mechanism:** This allows for precise resumption of the workflow and detailed error reporting with recovery suggestions.
*   **Implication for Integration:** This is more detailed than the current signal-based state updates managed by `orchestrator-pheromone-scribe`. Integrating this level of granularity would require significant changes to how `.roomodes` orchestrators manage and report on sub-task progress or a new layer of orchestration.

## 8. Pattern: User Intervention and Validation Points

*   **Description:** The `01_AI-RUN` workflow includes several explicit points where user validation or intervention is required or optional (e.g., validating `idea_document.md`, reviewing PRD, confirming template overwrites).
*   **Mechanism:** `02_AutoPilot.md` sets `pendingAction: "user_intervention_required"` or provides timed prompts for optional reviews.
*   **Implication for Integration:** `.roomodes` agents primarily operate autonomously once tasked. Incorporating these explicit user validation loops would require orchestrators to be ableto pause their workflow, signal for user input (perhaps via `ask_followup_question` or by tasking a specific "user interaction" mode if one existed), and then resume based on user feedback. This is a significant shift from the current model where user feedback typically triggers a new top-level task.

## 9. Pattern: Emphasis on UI/UX and Aesthetic Quality (`01_AI-RUN/07_Specs_Docs.md`)

*   **Description:** The `07_Specs_Docs.md` prompt places a strong emphasis on guiding the AI towards creating "beautiful, intuitive, and highly usable UI/UX," referencing a "Structured Summary of UI/UX Principles."
*   **Mechanism:** This involves populating `design_conventions.md` and feature specifications with detailed UI/UX considerations, drawing from foundational documents.
*   **Implication for Integration:** Relevant `.roomodes` agents (e.g., `spec-writer-feature-overview`, `architect-highlevel-module`, and any mode involved in UI generation or design documentation) must have their `customInstructions` updated to reflect this strong focus and to consult the appropriate foundational UI/UX principles.

## 10. Pattern: Codebase Xray (Initial Analysis)

*   **Description:** An early step in `01_AI-RUN` is the "In-Depth Codebase Understanding" or "Codebase Xray," producing `03_SPECS/codebase_xray_analysis.json`.
*   **Mechanism:** Uses a specific prompt ([`02_AI-DOCS/Documentation/Codebase_Xray_Prompt.md`](02_AI-DOCS/Documentation/Codebase_Xray_Prompt.md:1)) to analyze an existing codebase.
*   **Implication for Integration:** This is a distinct pre-processing or initial analysis task. A `.roomodes` agent, possibly `research-planner-strategic` or `code-comprehension-assistant-v2`, could be adapted or specifically tasked to perform this analysis at the beginning of a project if an existing codebase is involved. The output would then need to be registered in the `.pheromone` documentation registry.