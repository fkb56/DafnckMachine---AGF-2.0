# Practical Applications and Recommendations for `.roomodes` Integration

This document outlines practical applications of the integrated model and provides concrete recommendations for modifying `.roomodes` to support the `01_AI-RUN`, `02_AI-DOCS`, and `03_SPECS` workflows.

## 1. Activating the `01_AI-RUN` Workflow

*   **Trigger:** A user or a higher-level system could initiate the `01_AI-RUN` workflow by tasking the `uber-orchestrator` (or a new, dedicated "AI-RUN Workflow Orchestrator" mode if created).
*   **Initial Task Payload to Orchestrator:**
    *   `workflow_type: "AI_RUN"`
    *   `project_root: "/path/to/project"`
    *   `ai_run_prompts_dir: "01_AI-RUN/"` (or actual path)
    *   `ai_docs_templates_dir: "02_AI-DOCS/"`
    *   `specs_templates_dir: "03_SPECS/"`
    *   `initial_idea_brief: "User's initial project idea text"` (if starting from scratch)
    *   `current_ai_run_phase_override: null` (or a specific phase if resuming)
    *   `current_ai_run_step_override: null` (or a specific step if resuming)

## 2. Recommended Modifications to `.roomodes` Agents

The following are high-level recommendations. Specific line changes or detailed additions to `customInstructions` will be part of the "Final Report."

*   **`uber-orchestrator` (or new "AI-RUN Workflow Orchestrator"):**
    *   **New Logic:** Add capability to manage the `01_AI-RUN` phase sequence.
    *   **State Reading:** If a simplified `project_session_state.json` or `.ai_run_config.json` is used for this workflow, this orchestrator reads it to determine current phase/step or prompt file mappings. Otherwise, it relies on `.pheromone` signals for phase completion.
    *   **Delegation:** Task appropriate worker/sub-orchestrator modes for each `01_AI-RUN` phase, providing them with necessary inputs (e.g., paths to `01_AI-RUN` sub-prompts, paths to previously generated documents from `.pheromone`'s `documentation_registry`).
    *   **User Validation Handling:** Process responses from `ask_followup_question` initiated by worker modes for validation points.

*   **`research-planner-strategic`:**
    *   **Augmented `customInstructions`:**
        *   Accept a `phase_type` input (e.g., "IdeaGeneration", "MarketResearch", "CoreConceptDefinition").
        *   Based on `phase_type`, execute the logic of the corresponding `01_AI-RUN` sub-prompt (e.g., `03_Idea.md`, `04_Market_Research.md`, `05_Core_Concept.md`).
        *   Produce the specified output document (e.g., `idea_document.md` in `02_AI-DOCS/Project_Brief/`).
        *   Register the output document with the `orchestrator-pheromone-scribe` upon completion.
        *   Implement `ask_followup_question` for mandatory validation points as defined in `02_AutoPilot.md`.

*   **`spec-writer-feature-overview` (or new `prd-writer-mode`):**
    *   **Augmented `customInstructions`:**
        *   When tasked with "PRDGeneration" for the `01_AI-RUN` workflow:
            *   Copy [`01_AI-RUN/Template/PRD_template.md`](01_AI-RUN/Template/PRD_template.md:1) to `project_prd.md`.
            *   Populate `project_prd.md` based on `core_concept.md` and the structure of the template.
            *   Explicitly address PRD Section 5.2 (Design System) by eliciting user design preferences if not already clear, or by applying defaults.
            *   Register `project_prd.md` with the Scribe.

*   **New `orchestrator-technical-documentation` (Recommended):**
    *   **Role:** Manage the "Technical Specifications & Documentation" phase (`07_Specs_Docs.md` logic).
    *   **`customInstructions`:**
        *   Implement "Foolproof Template Copying" for documents in `02_AI-DOCS` and `03_SPECS`.
        *   Delegate creation/population of specific documents to:
            *   `architect-highlevel-module` (for `architecture.md`).
            *   `spec-writer-feature-overview` (for `feature_spec_FEAT-XXX.md`).
            *   `docs-writer-feature` (or new `conventions-writer-mode`) for `coding_conventions.md`, `design_conventions.md`.
        *   Instruct worker modes to consult and apply the "Structured Summary of UI/UX Principles" (derived from `02_AI-DOCS/Documentation/`).
        *   Ensure specific MCP calls (`context7`, `shadcn`, etc.) as per `07_Specs_Docs.md` are made by appropriate workers or itself.
        *   Create/update `03_SPECS/documentation_index.md`.
        *   Report overall phase completion to the Scribe.

*   **`coder-test-driven`:**
    *   **Augmented `customInstructions`:**
        *   When executing tasks derived from the `01_AI-RUN` workflow (specifically `08_Start_Building.md` logic):
            *   Perform project setup (CLI scaffolding, global styling) if it's an initial task.
            *   Implement the YC-style landing page as a priority.
            *   Adhere strictly to `coding_conventions.md` and `design_conventions.md`.
            *   Perform pre-flight checks for all specification documents relevant to the current task.
            *   Utilize MCPs in the prescribed order: `context7` for library/framework docs, then `shadcn` for UI components, then `@21st-dev/magic` for other UI needs/logos, then `github`/`firecrawl` for supplementary info.
            *   Maintain pixel-perfect UI implementation if applicable.

*   **`tester-tdd-master`:**
    *   **Augmented `customInstructions`:**
        *   When executing tasks for the `01_AI-RUN` "Testing" phase (`10_Testing.md` logic):
            *   Adopt "QualityGuardian" persona aspects.
            *   Execute a comprehensive test suite (unit, integration, functional, UI/UX, API, etc.) as defined in PRD and specs.
            *   Guide preview environment setup.
            *   Facilitate UAT using `ask_followup_question` to gather feedback.
            *   Manage issue reporting (potentially by requesting new bugfix tasks from an orchestrator).

*   **`devops-pipeline-manager`:**
    *   **Augmented `customInstructions`:**
        *   When executing tasks for the `01_AI-RUN` "Deployment" phase (`11_Deployment.md` logic):
            *   Adopt "DeployMaster" persona aspects.
            *   Follow `deployment_guide.md` for pre-deployment, deployment, and post-deployment verification steps.
            *   Implement rollback procedures if necessary.

*   **All relevant worker modes (e.g., `architect-highlevel-module`, `spec-writer-feature-overview`, `docs-writer-feature`):**
    *   **Augmented `customInstructions`:**
        *   Add logic to perform "template copying" if their task involves creating a document based on a template from `02_AI-DOCS` or `03_SPECS`.
        *   Explicitly refer to and apply principles from foundational documents like `AI_Design_Agent_Optimization.md` when creating relevant content (e.g., for `design_conventions.md` or UI sections of feature specs).

## 3. Data Flow and Communication

*   The `uber-orchestrator` (or equivalent) drives the `01_AI-RUN` sequence.
*   It tasks a phase-specific agent (e.g., `research-planner-strategic` for Market Research).
*   The tasked agent executes the logic of the corresponding `01_AI-RUN` sub-prompt.
*   Key document outputs are registered with `orchestrator-pheromone-scribe` and their paths stored in `.pheromone`'s `documentation_registry`.
*   The driving orchestrator consults `.pheromone` to get paths to these documents to pass as inputs to subsequent phase agents.
*   User validations are handled via `ask_followup_question`, with responses routed back to the driving orchestrator.

This model aims for a balance between leveraging the detailed `01_AI-RUN` workflow and integrating it pragmatically into the existing `.roomodes` structure.