# Recommendations for `.roomodes` Integration

Based on the detailed findings and in-depth analysis, this section provides specific, actionable recommendations for modifying the `.roomodes` file to integrate the `01_AI-RUN`, `02_AI-DOCS`, and `03_SPECS` workflows. These recommendations prioritize augmenting existing modes and aim to fulfill the user's request for targeted changes.

## 1. Overall Orchestration of the `01_AI-RUN` Workflow

*   **Recommendation:** Modify the **`uber-orchestrator`** mode.
*   **Rationale:** It already has responsibilities for reading project state (`.pheromone`) and delegating major pieces of work.
*   **Specific `customInstructions` Augmentations for `uber-orchestrator`:**
    *   Add logic to recognize a new top-level task type, e.g., "Execute AI-RUN Workflow".
    *   When this task is received, it should:
        *   Determine the current phase of the `01_AI-RUN` workflow. Initially, this would be "Getting Started". Subsequently, it would determine the next phase based on completion signals for the previous phase found in `.pheromone` (via the Scribe's `documentation_registry` updates).
        *   Consult an internal mapping (or a simple project config file like `.ai_run_config.json` if preferred for flexibility) to identify the standard `01_AI-RUN` sub-prompt filename for the current phase (e.g., `01_AI-RUN/01_Getting_Started.md`).
        *   Delegate the execution of this phase to the appropriate `.roomodes` agent (see recommendations below), passing the sub-prompt path, paths to any necessary input documents (retrieved from `.pheromone`'s `documentation_registry`), and context about the overall `01_AI-RUN` workflow.
        *   Handle user validation responses if a worker mode used `ask_followup_question`.
    *   **Targeted Change Example:** Add a new section to its decision logic: "If current high-level task is 'Execute AI-RUN Workflow', then: 1. Check `.pheromone` for last completed `01_AI-RUN` phase. 2. Determine next `01_AI-RUN` phase and its sub-prompt file (e.g., `01_AI-RUN/03_Idea.md`). 3. Task `research-planner-strategic` with executing this phase, providing the sub-prompt path and `idea_document.md` output path."

## 2. Phase-Specific Agent Modifications

*   **`code-comprehension-assistant-v2` (for "Getting Started - Codebase Xray")**
    *   **`customInstructions` Augmentation:** Add instructions to accept the path to [`02_AI-DOCS/Documentation/Codebase_Xray_Prompt.md`](02_AI-DOCS/Documentation/Codebase_Xray_Prompt.md:1) as a guiding document, and to save its JSON output to a specified path like `03_SPECS/codebase_xray_analysis.json`.

*   **`research-planner-strategic` (for "Idea Generation", "Market Research", "Core Concept Definition")**
    *   **`customInstructions` Augmentation:**
        *   Enable it to accept a `phase_type` parameter (e.g., "IdeaGeneration", "MarketResearch").
        *   Based on `phase_type`, it should follow the detailed logic within the corresponding `01_AI-RUN` sub-prompt (e.g., `01_AI-RUN/03_Idea.md`). This includes creating the specified output document (e.g., `idea_document.md`) at the correct location (e.g., `02_AI-DOCS/Project_Brief/`).
        *   Instruct it to use `ask_followup_question` for mandatory validation points defined in `02_AutoPilot.md` for these phases.
        *   Ensure its output summary to the Scribe clearly states the `01_AI-RUN` phase completed and the path to the created document.

*   **`spec-writer-feature-overview` (for "PRD Generation")**
    *   **`customInstructions` Augmentation:**
        *   When tasked with "PRDGeneration" for an `01_AI-RUN` workflow:
            *   Perform template copy: [`01_AI-RUN/Template/PRD_template.md`](01_AI-RUN/Template/PRD_template.md:1) to `project_prd.md`.
            *   Populate the copied `project_prd.md` using `core_concept.md` as primary input, strictly following the template's section structure.
            *   Pay special attention to PRD Section 5.2 (Design System), prompting for user design preferences if not detailed in `core_concept.md`.

*   **New Mode: `orchestrator-technical-documentation` (for "Technical Specifications & Documentation")**
    *   **Rationale:** The complexity of this phase (managing multiple template copies, diverse document types, specific MCP usage) warrants a dedicated orchestrator.
    *   **`roleDefinition`:** "Orchestrates the creation and population of all project-specific technical documents (architecture, conventions, feature specs, etc.) from templates, as per the `01_AI-RUN` 'Specs & Docs' phase. Manages delegation to specialized worker modes and ensures adherence to UI/UX principles."
    *   **`customInstructions`:**
        *   Implement the "Foolproof Template Copying" logic for all relevant templates in `02_AI-DOCS` and `03_SPECS`.
        *   Delegate population of specific documents:
            *   `architecture.md` to `architect-highlevel-module`.
            *   `feature_spec_FEAT-XXX.md` to `spec-writer-feature-overview`.
            *   `coding_conventions.md`, `design_conventions.md` to `docs-writer-feature` (or a new `conventions-writer-mode`).
        *   Instruct all delegated workers to consult and apply the "Structured Summary of UI/UX Principles" (derived from `02_AI-DOCS/Documentation/`).
        *   Manage the prescribed sequence of MCP calls (`context7`, `shadcn`, `@21st-dev/magic`, `github`, `firecrawl`) for information gathering, potentially by tasking itself or a specialized research/worker mode with these specific calls.
        *   Ensure creation/update of `03_SPECS/documentation_index.md`.
        *   Report overall phase completion to the Scribe.

*   **`uber-orchestrator` or `orchestrator-sparc-specification-master-test-plan` (for "Implementation Planning & Task Management")**
    *   **`customInstructions` Augmentation:** Add logic to parse `project_prd.md` and relevant generated specifications. Use the `taskmaster-ai` MCP (`parse_prd` or `add_task` tools) to generate `tasks/tasks.json` according to the structure in [`02_AI-DOCS/TaskManagement/Tasks_JSON_Structure.md`](02_AI-DOCS/TaskManagement/Tasks_JSON_Structure.md:1).

*   **`coder-test-driven` (for "Implementation")**
    *   **`customInstructions` Augmentation (Significant Additions Needed):**
        *   "When executing an `01_AI-RUN` 'Implementation' task:"
        *   "1. If this is the first coding task for the project, perform initial project setup: use the official CLI for the specified framework (e.g., `npx create-next-app`) to scaffold the project. Configure global styling (`global.css`, CSS resets, base typography) as per `design_conventions.md`."
        *   "2. Implement the Y Combinator-style landing page as a high-priority initial task, focusing on clarity, a strong CTA, and mobile-first responsiveness. Refer to `core_concept.md` and `project_prd.md` for messaging."
        *   "3. For all tasks, perform a pre-flight check: ensure all relevant specification documents (feature specs from `03_SPECS/features/`, `architecture.md`, `coding_conventions.md`, `design_conventions.md` from `02_AI-DOCS/`) are located (via `.pheromone` registry) and their content internalized."
        *   "4. Prioritize MCP usage for information: First, use `context7` for library/framework documentation. Then, use `shadcn` MCP for Shadcn/UI components (if applicable, using `add_item`). For other UI needs or inspiration, use `@21st-dev/magic` tools. Use `github` or `firecrawl` for supplementary information only if primary MCPs are insufficient."
        *   "5. Strictly adhere to `coding_conventions.md` for all code and `design_conventions.md` (and UI/UX principles) for all frontend/UI work, aiming for pixel-perfect implementation where designs are provided."
        *   (Existing instructions for TDD, self-reflection, Perplexity usage remain).

*   **`tester-tdd-master` (for "Testing")**
    *   **`customInstructions` Augmentation:**
        *   "When executing an `01_AI-RUN` 'Testing' task:"
        *   "Adopt the 'QualityGuardian' persona."
        *   "Review `project_prd.md` (Features, Use Cases, Test Strategy), feature specs in `03_SPECS/`, and task-specific `testStrategy` fields."
        *   "Execute comprehensive tests: unit, integration, functional (all user flows, data validation, error handling, boundary conditions, link integrity, interactive elements), UI/UX (responsiveness, visual consistency per `design_conventions.md`, accessibility, browser console checks), API, performance, and security tests as specified."
        *   "Guide the setup of a preview environment (staging, local, or platform preview) and provide user access instructions."
        *   "Facilitate User Acceptance Testing (UAT): Use `ask_followup_question` to present the preview and gather detailed user feedback on features and usability."
        *   "For issues found, clearly document them. If new bugfix tasks are needed, summarize the issue and recommend task creation to the orchestrator in your completion summary."
        *   "Verify fixes and conduct regression testing."

*   **`devops-pipeline-manager` (for "Deployment")**
    *   **`customInstructions` Augmentation:**
        *   "When executing an `01_AI-RUN` 'Deployment' task:"
        *   "Adopt the 'DeployMaster' persona."
        *   "Thoroughly review `project_prd.md` (Section 7: Deployment Plan) and the project-specific `02_AI-DOCS/Deployment/deployment_guide.md`."
        *   "Execute all pre-deployment preparations (environment config, final build, backup, dependency check)."
        *   "Follow `deployment_guide.md` to execute deployment steps, using platform-specific MCPs or CLI commands as specified."
        *   "Monitor deployment logs closely. If critical issues arise, initiate the documented rollback plan."
        *   "Perform post-deployment verification (smoke tests, health checks, monitoring review)."
        *   "Update `project_session_state.json` (conceptually, via signals to Scribe) upon successful deployment, including the live URL."

## 3. General Agent Instructions

*   **Template Handling:** All worker modes that might create documents from `02_AI-DOCS` or `03_SPECS` templates must have instructions added to their `customInstructions` to:
    1.  Receive a source template path and a target instance path.
    2.  Copy the template to the target path.
    3.  Populate the *copied* instance, not the original template.
*   **Consulting Foundational UI/UX Principles:** Modes involved in design, UI, or specification of UI-heavy features (e.g., `spec-writer-feature-overview`, `architect-highlevel-module`, `coder-test-driven` when doing UI) must be instructed to consult and apply principles from `02_AI-DOCS/Documentation/AI_Design_Agent_Optimization.md` and `02_AI-DOCS/Documentation/Optimizing_the_Design_Process.md` (or a compiled summary of these).
*   **Document Registration:** All modes creating significant documents as part of the `01_AI-RUN` workflow must clearly state the document's creation and path in their summary to the `orchestrator-pheromone-scribe` so it can be added to the `documentation_registry`.

By implementing these targeted augmentations, the `.roomodes` agents can effectively execute the `01_AI-RUN` workflow, leveraging its structured approach while fitting within the existing swarm architecture.