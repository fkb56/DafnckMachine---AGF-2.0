# Identified Contradictions and Discrepancies

This document will list any contradictions or significant discrepancies found between the `01_AI-RUN` workflow, the `02_AI-DOCS`/`03_SPECS` documentation system, and the existing `.roomodes` agent definitions.

## Initial Potential Areas of Discrepancy (To Be Verified)

1.  **State Management Granularity:**
    *   **`01_AI-RUN` (`02_AutoPilot.md`):** Proposes a highly granular state management system using `project_session_state.json` with detailed `lastCompletedStep` markers (e.g., `idea_generation_file_saved`, `specsDocsPhase_copiedArchitectureTemplate`).
    *   **`.roomodes`:** Primarily relies on the `.pheromone` file for higher-level signals and a documentation registry. Orchestrators are generally stateless beyond their immediate task inputs and reading `.pheromone`.
    *   **Potential Contradiction/Gap:** Directly implementing the `01_AI-RUN` state model within the current `.roomodes` pheromone-centric approach might be complex or require a new state management layer/convention for agents executing this specific workflow.

2.  **Persona Adoption:**
    *   **`01_AI-RUN` (`02_AutoPilot.md`):** Describes dynamic persona adoption by the main orchestrator ("ProjectArchitect AI") based on the sub-prompt for each phase.
    *   **`.roomodes`:** Agents have fixed personas defined in their `slug`, `name`, and `roleDefinition`.
    *   **Potential Contradiction/Gap:** Dynamic persona switching is not a native feature of the current `.roomodes` structure. Integration would require either mapping phases to existing fixed-persona modes or a new mechanism.

3.  **User Intervention Points:**
    *   **`01_AI-RUN` (`02_AutoPilot.md`):** Defines several explicit user validation and intervention points, some mandatory, some optional with timeouts.
    *   **`.roomodes`:** Agents generally operate autonomously once tasked, with user interaction typically occurring at the beginning or end of a task chain, or via `ask_followup_question` for specific clarifications.
    *   **Potential Contradiction/Gap:** The `01_AI-RUN` model of pausing for user validation mid-workflow is different from the typical `.roomodes` operational flow.

4.  **MCP Tool Invocation Specificity:**
    *   **`01_AI-RUN` (`07_Specs_Docs.md`, `08_Start_Building.md`):** Prescribes very specific MCP tool usage sequences and priorities (e.g., `context7` first for docs, then `github`/`firecrawl`).
    *   **`.roomodes`:** Some modes have general MCP permissions or mandates (e.g., `coder-test-driven` using Perplexity), but not usually with such a detailed, pre-defined selection and order for a variety of MCPs within a single phase's instructions.
    *   **Potential Contradiction/Gap:** `customInstructions` for relevant `.roomodes` agents will need to be significantly augmented to include this detailed MCP usage logic.

5.  **Error Handling and Recovery:**
    *   **`01_AI-RUN` (`02_AutoPilot.md`):** Details a structured `errorState` object with `errorType`, `errorMessage`, `failedStep`, and `recoverySuggestion`.
    *   **`.roomodes`:** Error handling is typically managed by the orchestrator receiving a failed task completion from a worker, or a worker reporting an issue in its summary. The structured recovery suggestion mechanism is less explicit.
    *   **Potential Contradiction/Gap:** Aligning the detailed error reporting and recovery suggestion model of `01_AI-RUN` with the existing `.roomodes` error handling patterns.

Further contradictions may be identified as the analysis deepens and specific integration points are mapped.