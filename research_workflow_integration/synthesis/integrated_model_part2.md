# Integrated Model for Workflow Execution in `.roomodes` (Part 2)

This document continues proposing an integrated model for incorporating the `01_AI-RUN` workflows into the `.roomodes` framework, addressing further knowledge gaps.

## 3. Addressing User Intervention and Validation Loops

**Challenge:** `01_AI-RUN` includes explicit user validation points, contrasting with the generally autonomous `.roomodes` agents.

**Proposed Integration Strategy:**

*   **Leverage `ask_followup_question` for Mandatory Validation:**
    *   When a `.roomodes` agent completes a phase corresponding to a *mandatory* validation point in `01_AI-RUN` (e.g., after "Idea Generation" or "Core Concept Definition"), its `customInstructions` will direct it to use the `ask_followup_question` tool.
    *   The question posed would be: "Phase [Phase Name] is complete. The output document [Document Name] is available at [path]. Please review and confirm if it meets requirements to proceed to the next phase: [Next Phase Name]."
    *   Suggested answers could be: "Yes, proceed to [Next Phase Name]." or "No, revisions are needed for [Document Name]."
    *   The orchestrator that tasked this agent (e.g., `uber-orchestrator`) would receive the user's response and decide the next action (proceed or re-task for revision).
*   **Timed Optional Reviews - Simplified Approach:**
    *   The `01_AI-RUN` concept of a 60-second timeout for optional reviews is hard to implement directly in the current asynchronous `.roomodes` model without a persistent timer mechanism.
    *   **Simplification:** For phases with "Conditional Optional Review" (e.g., after Market Research or PRD Generation), the `.roomodes` agent completing the phase will, in its natural language summary to the Scribe (and thus visible to humans monitoring `.pheromone`), state: "Phase [Phase Name] complete. Output [Document Name] at [path] is ready. The workflow will proceed to [Next Phase Name] unless a new directive for review or revision is issued."
    *   This places the onus on a human supervisor or a higher-level orchestrator to intervene with a new task if a review is desired before the `uber-orchestrator` naturally picks up the next phase based on the completion signal.
*   **Template Overwrite Confirmation:**
    *   During the "Specs & Docs" phase, if a `.roomodes` agent (e.g., an adapted `spec-writer-feature-overview` or `architect-highlevel-module`) detects that a target file for a template copy already exists, its `customInstructions` must direct it to use `ask_followup_question`.
    *   Question: "Target file [target_path] for [Document Type] already exists. How should I proceed?"
    *   Suggestions: "Overwrite the existing file.", "Use the existing file (skip template copy for this item).", "Halt this documentation step and report an error."

**Recommendation for `.roomodes` Modification:**
*   Update `customInstructions` for modes responsible for `01_AI-RUN` phases that have mandatory validation points to use `ask_followup_question`.
*   For optional reviews, rely on clear natural language summaries indicating intent to proceed, allowing for human/orchestrator intervention.

## 4. Addressing Precise Mapping of `01_AI-RUN` Phases to `.roomodes` Agents

**Challenge:** A detailed mapping is needed to assign `01_AI-RUN` phase responsibilities to specific `.roomodes` agents and define necessary instruction changes.

**Proposed Integration Strategy & Mapping (High-Level - details per mode in subsequent synthesis docs):**

This will be an iterative process. The general approach is to assign an `01_AI-RUN` phase to an existing `.roomodes` agent whose core competency aligns. The agent's `customInstructions` will then be augmented with the specific logic, inputs, outputs, and MCP usage patterns of that `01_AI-RUN` phase/sub-prompt.

*   **Phase 1: Getting Started (incl. Codebase Xray)**
    *   **Orchestration:** `uber-orchestrator` initiates.
    *   **Codebase Xray Task:** Delegate to `code-comprehension-assistant-v2`.
        *   *Modification:* `customInstructions` to accept the [`02_AI-DOCS/Documentation/Codebase_Xray_Prompt.md`](02_AI-DOCS/Documentation/Codebase_Xray_Prompt.md:1) as a guiding document for its analysis and to output to `03_SPECS/codebase_xray_analysis.json`.
    *   **User Input/Initial State:** Handled by `uber-orchestrator` or a new lightweight "ProjectInitializer" mode if interaction is complex.

*   **Phase 2-4: Idea Generation, Market Research, Core Concept Definition**
    *   **Agent:** `research-planner-strategic`.
    *   *Modification:* `customInstructions` to accept a "phase_type" input (Idea, MarketResearch, CoreConcept). Based on this, it follows the logic of the corresponding `01_AI-RUN` sub-prompt (`03_Idea.md`, `04_Market_Research.md`, `05_Core_Concept.md`), produces the specified output document (e.g., `idea_document.md`), and uses `ask_followup_question` for mandatory validation points.

*   **Phase 5: PRD Generation**
    *   **Agent:** `spec-writer-feature-overview` (adapted) or a new `prd-writer-mode`.
    *   *Modification:* `customInstructions` to follow the structure of [`01_AI-RUN/Template/PRD_template.md`](01_AI-RUN/Template/PRD_template.md:1) (by copying it to `project_prd.md` and populating) using `core_concept.md` as input. Emphasize eliciting design preferences for PRD Section 5.2.

*   **Phase 6: Technical Specifications & Documentation (`07_Specs_Docs.md` logic)**
    *   **Orchestration:** A dedicated task orchestrator, potentially `orchestrator-sparc-specification-master-test-plan` (if its scope is broadened beyond just SPARC spec) or a new `orchestrator-technical-documentation`.
    *   This orchestrator will manage the "Foolproof Template Copying" and population for various documents.
    *   It will delegate creation of specific documents to:
        *   `architect-highlevel-module` for `architecture.md`.
        *   `spec-writer-feature-overview` for `feature_spec_FEAT-XXX.md`.
        *   `docs-writer-feature` (or a new `conventions-writer-mode`) for `coding_conventions.md` and `design_conventions.md`.
    *   *Modification:* All these worker modes need `customInstructions` to understand they might be working from a copied template and to integrate UI/UX principles from the "Structured Summary" when relevant. The orchestrator needs instructions for the template copying logic and specific MCP calls from `07_Specs_Docs.md`.

*   **Phase 7: Implementation Planning & Task Management**
    *   **Agent:** `uber-orchestrator` or `orchestrator-sparc-specification-master-test-plan` (if it's also responsible for breaking down its MPP).
    *   *Modification:* Instructions to parse `project_prd.md` and created specs, then use `taskmaster-ai` MCP's `parse_prd` or `add_task` tools to populate `tasks/tasks.json` according to [`02_AI-DOCS/TaskManagement/Tasks_JSON_Structure.md`](02_AI-DOCS/TaskManagement/Tasks_JSON_Structure.md:1).

*   **Phase 8: Implementation (`08_Start_Building.md` logic)**
    *   **Orchestration:** `orchestrator-feature-implementation-tdd`.
    *   **Coding Task:** `coder-test-driven`.
    *   *Modification:* `coder-test-driven`'s `customInstructions` augmented significantly with:
        *   Project setup logic (CLI scaffolding, global styling).
        *   Landing page creation guidelines.
        *   Prioritized MCP usage (`context7` first, then `shadcn`, `@21st-dev/magic`).
        *   Strict adherence to `design_conventions.md` and `coding_conventions.md`.
        *   Pre-flight check for spec documents.

*   **Phase 9: Testing (`10_Testing.md` logic)**
    *   **Agent:** `tester-tdd-master`.
    *   *Modification:* `customInstructions` expanded to include:
        *   "QualityGuardian" persona aspects.
        *   Comprehensive test execution (unit, integration, functional, UI/UX, API, performance, security).
        *   Preview environment setup guidance.
        *   UAT facilitation (using `ask_followup_question` for feedback).
        *   Issue tracking (potentially by creating bugfix tasks via an orchestrator).

*   **Phase 10: Deployment (`11_Deployment.md` logic)**
    *   **Agent:** `devops-pipeline-manager`.
    *   *Modification:* `customInstructions` to include:
        *   "DeployMaster" persona aspects.
        *   Pre-deployment checklist.
        *   Execution of steps from `deployment_guide.md`.
        *   Post-deployment verification and smoke testing.
        *   Rollback plan execution if needed.

**Recommendation for `.roomodes` Modification:**
*   Focus on augmenting `customInstructions` of existing modes.
*   A new `orchestrator-technical-documentation` might be beneficial for the complexity of Phase 6.
*   The `uber-orchestrator` will likely need enhanced logic to drive the overall `01_AI-RUN` sequence if not creating a new top-level "AI-RUN Orchestrator".

This detailed mapping will be further refined, with specific line changes proposed in later synthesis documents.