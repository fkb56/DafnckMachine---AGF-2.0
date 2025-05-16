# Integrated Model for Workflow Execution in `.roomodes` (Part 3)

This document concludes the proposed integrated model for incorporating the `01_AI-RUN` workflows into the `.roomodes` framework, addressing the final set of identified knowledge gaps.

## 5. Addressing Integration of "Structured Summary of UI/UX Principles"

**Challenge:** `01_AI-RUN/07_Specs_Docs.md` mandates the use of a "Structured Summary of UI/UX Principles" (derived from foundational documents in `02_AI-DOCS/Documentation/`) to guide the creation of design-related project documents.

**Proposed Integration Strategy:**

*   **Centralized Access to Principles:**
    *   The "Structured Summary of UI/UX Principles" should ideally be a well-defined, accessible artifact. Since it's derived from existing files (`AI_Design_Agent_Optimization.md`, etc.), the `uber-orchestrator` or the orchestrator initiating the "Specs & Docs" phase could be responsible for ensuring this summary is available, perhaps by instructing a worker mode to synthesize it once and store it in a known location within `02_AI-DOCS/Documentation/` (e.g., `ui_ux_compiled_principles.md`).
    *   Alternatively, and more aligned with current `.roomodes` capabilities, the `customInstructions` of relevant worker modes can explicitly list the key principles or refer to the *original* foundational documents directly (e.g., "When creating design conventions, refer to the principles outlined in `02_AI-DOCS/Documentation/AI_Design_Agent_Optimization.md` and `02_AI-DOCS/Documentation/Optimizing_the_Design_Process.md` to ensure clarity, consistency, and user-centricity.").
*   **Explicit Instruction in `customInstructions`:**
    *   For `.roomodes` agents like `spec-writer-feature-overview` (when creating feature specs with UI elements), `architect-highlevel-module` (when considering UI/UX impact of architecture), and especially any mode tasked with creating/populating `design_conventions.md`:
        *   Their `customInstructions` must be updated to explicitly require adherence to these UI/UX principles.
        *   Example addition: "When generating UI specifications or design conventions, you MUST consult and apply the UI/UX best practices and principles outlined in [path to summary or foundational docs, e.g., `02_AI-DOCS/Documentation/AI_Design_Agent_Optimization.md`]. Ensure your output promotes clarity, consistency, user control, feedback, efficiency, accessibility, and a strong visual hierarchy, aligning with modern design aesthetics."
*   **Cross-referencing in Outputs:**
    *   Generated documents like `design_conventions.md` and feature specifications should, where appropriate, reference specific principles or foundational documents to justify design decisions.

**Recommendation for `.roomodes` Modification:**
*   Modify `customInstructions` of `spec-writer-feature-overview`, `architect-highlevel-module`, and any mode creating `design_conventions.md` to explicitly reference and require application of principles from `02_AI-DOCS/Documentation/AI_Design_Agent_Optimization.md`, `02_AI-DOCS/Documentation/Optimizing_the_Design_Process.md`, and relevant sections of `coding_conventions_template.md` (which also touches on UI/UX).
*   The `orchestrator-technical-documentation` (proposed in Part 2) would ensure these instructions are passed to the relevant worker modes.

## 6. Addressing Handling of `filenameMapping`

**Challenge:** `02_AutoPilot.md` uses `project_session_state.json.filenameMapping` to map logical prompt names (e.g., "MarketResearchPrompt") to actual filenames (e.g., `04_Market_Research.md`).

**Proposed Integration Strategy:**

*   **Convention Over Configuration (Preferred for `.roomodes`):**
    *   The `01_AI-RUN` directory structure and filenames are already quite consistent (e.g., `01_Getting_Started.md`, `03_Idea.md`, `04_Market_Research.md`).
    *   Instead of relying on a separate `filenameMapping` within a state file, the orchestrator managing the `01_AI-RUN` workflow (e.g., `uber-orchestrator` or a new dedicated one) can be hardcoded or configured with the standard sequence and corresponding filenames.
    *   For example, it knows that after the "Idea" phase (which uses `01_AI-RUN/03_Idea.md` logic and produces `idea_document.md`), the next phase is "Market Research" which uses `01_AI-RUN/04_Market_Research.md` logic.
*   **Simplified Mapping if Necessary:**
    *   If some flexibility is still desired (e.g., user renames `03_Idea.md` to `MyProject_Idea_Prompt.md`), a very simple, top-level configuration file within the project (e.g., `.ai_run_config.json`) could hold these mappings. The primary orchestrator would read this once. This avoids embedding it deep within a frequently changing state file.
    *   `project_session_state.json` as described in `02_AutoPilot.md` is more for dynamic state *during* execution, not static configuration of prompt files.

**Recommendation for `.roomodes` Modification:**
*   The orchestrator mode responsible for driving the `01_AI-RUN` workflow should have the sequence of logical phases and their corresponding standard prompt filenames (e.g., `01_AI-RUN/03_Idea.md` for the "IdeaPrompt" phase) defined within its `customInstructions` or a simple, readable internal mapping.
*   This largely obviates the need for the dynamic `filenameMapping` field from `project_session_state.json` for this specific purpose.

## 7. General Recommendations for `.roomodes` Modifications

*   **Targeted Augmentation:** Prioritize augmenting the `customInstructions` of existing, well-aligned `.roomodes` agents rather than creating many new, narrowly focused modes, unless a clear gap in capability exists (e.g., the proposed `orchestrator-technical-documentation`).
*   **Clarity of Responsibility:** Ensure that for each phase of the `01_AI-RUN` workflow, it's clear which `.roomodes` agent is responsible and that its instructions are updated to reflect the specific logic, inputs, outputs, and MCP usage patterns of that phase.
*   **User Request for Targeted Changes:** The user requested "target specific lines for replacement... avoid rewriting the entire document." This means proposed changes to `.roomodes` should be presented as specific additions or modifications to existing `customInstructions` sections, rather than complete rewrites of mode definitions, where feasible. Regex patterns or line number ranges will be identified in the "Final Report" recommendations.
*   **Leverage `.pheromone` Documentation Registry:** The `documentation_registry` in `.pheromone` should be the primary mechanism for tracking paths to key generated documents (e.g., `idea_document.md`, `project_prd.md`, `architecture.md`). Orchestrators and workers should be instructed to consult this registry.
*   **AI Verifiable Outcomes:** Maintain the `.roomodes` emphasis on AI verifiable outcomes. The tasks defined within the `01_AI-RUN` workflow (e.g., creation of a specific document, successful execution of a script) generally align with this.

This concludes the synthesis of the integrated model. The next step is to compile the final report.