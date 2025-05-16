# Integrated Model for Workflow Execution in `.roomodes` (Part 1)

This document proposes an integrated model for incorporating the `01_AI-RUN`, `02_AI-DOCS`, and `03_SPECS` workflows into the existing `.roomodes` agent framework. It aims to address the key knowledge gaps identified during the analysis phase.

## 1. Addressing State Management Reconciliation

**Challenge:** The `01_AI-RUN` workflow uses a granular, file-based state (`project_session_state.json`) while `.roomodes` primarily uses `.pheromone` for higher-level signals and is generally stateless for orchestrators beyond task inputs.

**Proposed Integration Strategy:**

Instead of fully replicating `project_session_state.json` management within each `.roomodes` agent, we propose a hybrid approach:

*   **Leverage `.pheromone` for High-Level Phase Tracking:**
    *   The `orchestrator-pheromone-scribe` can be enhanced. When an orchestrator responsible for an `01_AI-RUN`-style phase (e.g., "Market Research Phase") reports completion, its natural language summary should explicitly state the phase completed and key outputs (document paths).
    *   The Scribe's `interpretationLogic` (in `.swarmConfig`) could be updated to recognize these phase completion signals and update the `documentation_registry` in `.pheromone` with paths to major artifacts generated during that phase (e.g., `idea_document.md`, `market_research_report.md`). This makes `.pheromone` the source of truth for *completed phase outputs*.

*   **Introduce a "Workflow Context Object" for In-Phase Granular State:**
    *   For orchestrators managing multi-step `01_AI-RUN` phases (like the "Specs & Docs" phase or the main "AutoPilot" logic if a single orchestrator handles it), they will need to manage a temporary, in-memory context object that mirrors the *necessary* parts of `project_session_state.json` relevant *only to their current, active phase*.
    *   This context object would track sub-steps within that phase (e.g., `specsDocsPhase_copiedArchitectureTemplate`, `specsDocsPhase_populatedArchitectureDoc`).
    *   **Persistence:** If an orchestrator's task is interrupted or needs to be resumable across multiple agent invocations (which is not typical for current `.roomodes` orchestrators but is implied by `02_AutoPilot.md`'s granularity), this temporary context object could be:
        1.  Passed along in the `task_completion` payload of the worker it delegates to, and received back. (Less robust for orchestrator failure).
        2.  Written to a temporary file in a designated project workspace area (e.g., `.tmp_workflow_state/phase_X_context.json`) by the orchestrator at the end of its turn if the phase is not yet complete. The orchestrator would then need logic to load this upon re-activation for the same overarching phase. This is a significant addition to current `.roomodes` behavior.
        3.  A simpler approach for `.roomodes`: The orchestrator for a complex phase (like "Specs & Docs") breaks it down into a sequence of *sub-tasks* it delegates one by one. The completion of each sub-task (e.g., "Create Architecture Document from Template", "Populate Architecture Document") would be a signal in `.pheromone`. The orchestrator then knows which sub-task is next. This avoids complex file-based state for the orchestrator itself.

*   **`filenameMapping`:**
    *   This can be handled by the primary orchestrator responsible for initiating the `01_AI-RUN` style workflow. It could read a simplified mapping from a project configuration file (or have it hardcoded if the `01_AI-RUN` structure is fixed) and pass the correct prompt filenames to worker modes responsible for executing those phases.

*   **Error Handling:**
    *   The structured `errorState` from `02_AutoPilot.md` is valuable. When a `.roomodes` agent encounters an error executing an `01_AI-RUN` step, its natural language summary to the Scribe should include these details (`errorType`, `errorMessage`, `failedStep`). The Scribe can then record this in the `.pheromone` signal. Recovery suggestions would primarily guide the `uber-orchestrator` or a human reviewer.

**Recommendation for `.roomodes` Modification:**
*   The `uber-orchestrator` (or a new, dedicated "AI-RUN Workflow Orchestrator" mode) would be responsible for managing the overall sequence of the `01_AI-RUN` phases.
*   It would read the `.pheromone` file to see which major artifacts/phases are complete.
*   It would then task the appropriate existing `.roomodes` worker/orchestrator (e.g., `research-planner-strategic` for "Market Research", `spec-writer-feature-overview` adapted for "PRD Generation") with the *next logical phase* from `01_AI-RUN`.
*   The `customInstructions` for these tasked modes would need to be augmented to include the specific logic of that `01_AI-RUN` phase (e.g., for `07_Specs_Docs.md`, the logic for template copying and population).
*   Granular `lastCompletedStep` within a complex phase (like `07_Specs_Docs.md`) would be managed internally by the mode executing that phase, or by breaking that phase into multiple distinct tasks delegated sequentially.

## 2. Addressing Dynamic Persona Adoption

**Challenge:** `01_AI-RUN` suggests dynamic persona adoption, while `.roomodes` agents have fixed personas.

**Proposed Integration Strategy:**

*   **Option A: Map Phases to Best-Fit Existing Personas:**
    *   Identify the `.roomodes` agent whose existing persona (`name` and `roleDefinition`) most closely aligns with the persona described for each `01_AI-RUN` phase (e.g., "MarketStrategist AI" for market research maps well to `research-planner-strategic`).
    *   The orchestrating mode (e.g., `uber-orchestrator`) would delegate the phase to this best-fit agent. The agent executes using its standard persona, but its `customInstructions` would be augmented with the specific tasks and objectives of that `01_AI-RUN` phase.
    *   This is the least disruptive approach to `.roomodes`.

*   **Option B: Persona Guidance in Tasking (Lightweight Adoption):**
    *   When an orchestrator tasks a worker mode for an `01_AI-RUN` phase, the task instructions could include a line like: "For this task, please adopt the communication style and focus of a [Persona Name, e.g., 'MarketStrategist AI']. Your primary objective is [phase objective from sub-prompt]."
    *   The worker mode would still operate under its main `roleDefinition` but would use this as guidance for its output and interaction style for that specific task. This relies on the LLM's ability to adapt its style based on instruction.

*   **Option C: Introduce a "Generic Phase Executor" Mode (More Complex):**
    *   A new, highly flexible worker mode could be created, designed to take a sub-prompt file path (e.g., `01_AI-RUN/04_Market_Research.md`) and a target persona string as input. It would then attempt to execute the sub-prompt *as if* it were that persona. This is more complex to implement reliably.

**Recommendation for `.roomodes` Modification:**
*   Primarily rely on **Option A**. Augment the `customInstructions` of existing, well-aligned modes (like `research-planner-strategic`, `spec-writer-feature-overview`, `architect-highlevel-module`, `coder-test-driven`, `tester-tdd-master`, `devops-pipeline-manager`) to include the specific logic, inputs, outputs, and MCP usage patterns for the `01_AI-RUN` phases they are best suited to execute.
*   For example, when `research-planner-strategic` is tasked with the "Market Research" phase from `01_AI-RUN`, its `customInstructions` should guide it to follow the structure and objectives outlined in `01_AI-RUN/04_Market_Research.md`, including producing `market_research.md`.
*   The `name` and `roleDefinition` of the chosen `.roomodes` agent would serve as its effective persona for that phase. The key is that its *actions* align with the `01_AI-RUN` sub-prompt.

This covers the initial synthesis for state management and persona adoption. Part 2 will address user intervention, precise mapping, and other gaps.