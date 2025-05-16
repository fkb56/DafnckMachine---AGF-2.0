# Critical Knowledge Gaps for Workflow Integration

This document identifies critical knowledge gaps and areas requiring further clarification or research to successfully integrate the `01_AI-RUN`, `02_AI-DOCS`, and `03_SPECS` workflows into the `.roomodes` agent definitions.

## 1. State Management Reconciliation

*   **Gap:** The `01_AI-RUN` workflow relies on a detailed, file-based state (`project_session_state.json`) with granular `lastCompletedStep` tracking. The existing `.roomodes` system uses `.pheromone` for higher-level signals and a document registry, with orchestrators being largely stateless.
*   **Question:** What is the most effective and least disruptive strategy to reconcile these two state management approaches?
    *   Should relevant `.roomodes` orchestrators be adapted to read/write a `project_session_state.json` when executing an `01_AI-RUN`-style workflow?
    *   Can the `.pheromone` file's signal structure be enhanced to accommodate the required granularity of `lastCompletedStep` for this specific workflow, perhaps with a new signal type or payload structure?
    *   Is a new, dedicated "Workflow State Manager" mode or MCP service required to handle `project_session_state.json` interactions, which other modes would then query?
*   **Information Needed:** Deeper understanding of the performance and complexity implications of each approach. Best practices for managing granular workflow state in multi-agent systems that also use a global signal/event bus like `.pheromone`.

## 2. Dynamic Persona Adoption Mechanism

*   **Gap:** `01_AI-RUN` describes dynamic persona adoption by its orchestrator based on sub-prompts. `.roomodes` agents have fixed personas.
*   **Question:** How can dynamic persona adoption be implemented or simulated within the `.roomodes` framework for agents executing the `01_AI-RUN` workflow?
    *   Can an orchestrator mode dynamically alter parts of its `customInstructions` or internal logic based on the current `01_AI-RUN` phase?
    *   Is it more feasible to map each `01_AI-RUN` phase (and its associated persona) to a distinct, specialized `.roomodes` agent, potentially requiring new, narrowly focused modes?
    *   Could the `uber-orchestrator` manage "persona context" and pass it as an input to worker modes, which then adapt their communication style?
*   **Information Needed:** Feasibility and complexity of modifying mode behavior dynamically versus expanding the number of specialized modes.

## 3. User Intervention and Validation Loop Implementation

*   **Gap:** `01_AI-RUN` specifies several explicit user validation points. `.roomodes` agents are primarily autonomous after tasking.
*   **Question:** What is the best way to implement user validation loops within the `.roomodes` execution model for the `01_AI-RUN` workflow?
    *   Can orchestrator modes use the `ask_followup_question` tool to pause and solicit user validation at specific points, then resume based on the response?
    *   Would it require a dedicated "User Interaction" or "Validation Gateway" mode that orchestrators delegate to when user input is needed?
    *   How would timeouts for optional reviews (as described in `02_AutoPilot.md`) be managed?
*   **Information Needed:** Technical capabilities and limitations of existing tools like `ask_followup_question` for managing multi-step validation dialogues. Design patterns for incorporating synchronous user feedback into asynchronous agent workflows.

## 4. Precise Mapping of `01_AI-RUN` Phases to `.roomodes` Agents

*   **Gap:** While initial alignments (Primary Findings Part 3, Q3.2) have been identified, a detailed, step-by-step mapping of each `01_AI-RUN` phase and its sub-actions to specific `.roomodes` agents (and their necessary modifications) is still needed.
*   **Question:** For each phase in `01_AI-RUN` (e.g., "Idea Generation", "Specs & Docs", "Implementation"), which existing `.roomodes` agent is the best fit? What specific new instructions or logic (e.g., template copying, specific MCP calls, UI/UX focus) must be added to that agent's `customInstructions`?
*   **Information Needed:** A granular cross-walk between `01_AI-RUN` phase objectives/actions and the detailed capabilities/instructions of each `.roomodes` agent. This will likely be an iterative process during the "Synthesis" phase.

## 5. Integration of "Structured Summary of UI/UX Principles"

*   **Gap:** `01_AI-RUN/07_Specs_Docs.md` mandates the use of a "Structured Summary of UI/UX Principles" (derived from `02_AI-DOCS/Documentation/`) to guide the creation of design-related documents.
*   **Question:** How can relevant `.roomodes` agents (e.g., `spec-writer-feature-overview`, `architect-highlevel-module`, any UI-generating mode) be reliably instructed to:
    *   Access or "internalize" this summary/these principles?
    *   Consistently apply these principles when generating content for `design_conventions.md`, feature specs, etc.?
*   **Information Needed:** Best practices for embedding or referencing such guiding principle documents within agent instructions to ensure consistent application.

## 6. Handling of `filenameMapping`

*   **Gap:** `02_AutoPilot.md` uses `project_session_state.json.filenameMapping` to map logical prompt names to actual filenames.
*   **Question:** If the `01_AI-RUN` workflow is integrated, how will this mapping be managed?
    *   Will the `.roomodes` agent responsible for orchestrating this workflow need to read/use this mapping?
    *   Could this be simplified by standardizing filenames within the `01_AI-RUN` directory itself, reducing reliance on a separate mapping?
*   **Information Needed:** Clarity on whether the flexibility of `filenameMapping` is essential or if a convention-over-configuration approach is preferable for `.roomodes` integration.

Addressing these knowledge gaps will be crucial for developing a robust and effective integration plan. This may involve formulating targeted queries for an AI search tool (conceptually) or making reasoned assumptions based on the provided documentation if direct answers are not available.