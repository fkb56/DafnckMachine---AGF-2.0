# Information Sources for Workflow Integration Research

This document outlines the primary information sources that will be consulted to answer the key research questions regarding the integration of `01_AI-RUN`, `02_AI-DOCS`, and `03_SPECS` workflows into the `.roomodes` agent definitions.

## 1. Core Workflow Definition and Orchestration

*   **Source File:** `01_AI-RUN/01_Getting_Started.md`
    *   **Relevance:** Provides the overall workflow overview, phase descriptions, file naming conventions, and initial AI agent onboarding instructions (including the Codebase Xray directive). Key for understanding the intended sequence and interaction of workflow components.
*   **Source File:** `01_AI-RUN/02_AutoPilot.md`
    *   **Relevance:** Details the automated workflow orchestration, state management via `project_session_state.json`, error handling, persona management, internal prompt execution process, and specific phase logic. This is crucial for understanding the dynamic execution of the `01_AI-RUN` workflow.
*   **Source Files:** `01_AI-RUN/03_Idea.md`, `01_AI-RUN/04_Market_Research.md`, `01_AI-RUN/05_Core_Concept.md`, `01_AI-RUN/06_PRD_Generation.md`, `01_AI-RUN/07_Specs_Docs.md`, `01_AI-RUN/08_Start_Building.md`, `01_AI-RUN/10_Testing.md`, `01_AI-RUN/11_Deployment.md`
    *   **Relevance:** These files represent the individual phase prompts within the `01_AI-RUN` workflow. They define the objectives, inputs, outputs, and AI persona for each stage. They are essential for understanding the specific tasks and logic to be integrated.
*   **Source File:** `01_AI-RUN/09_Task_Manager.md` (and its referenced documents)
    *   **Relevance:** Points to `02_AI-DOCS/TaskManagement/Roo_Task_Workflow.md` and `02_AI-DOCS/TaskManagement/Tasks_JSON_Structure.md`, which are critical for understanding how tasks are generated, structured, and managed.

## 2. Documentation Structure, Templates, and Content Guidance

*   **Source Directory:** `02_AI-DOCS/` (recursive listing)
    *   **Relevance:** Contains templates for project-specific documentation (e.g., `architecture_template.md`, `coding_conventions_template.md`, `design_conventions_template.md`) and core AI guidance documents (e.g., `AI_Design_Agent_Optimization.md`, `AI_Coding_Agent_Optimization.md`, `Codebase_Xray_Prompt.md`). Essential for understanding the "template-to-instance" pattern and the expected content of generated documents.
    *   Specific attention will be paid to:
        *   `02_AI-DOCS/Documentation/AI_Design_Agent_Optimization.md`
        *   `02_AI-DOCS/Documentation/AI_Coding_Agent_Optimization.md`
        *   `02_AI-DOCS/Documentation/Codebase_Xray_Prompt.md`
        *   `02_AI-DOCS/TaskManagement/Roo_Task_Workflow.md`
        *   `02_AI-DOCS/TaskManagement/Tasks_JSON_Structure.md`
        *   All `*_template.md` files within subdirectories.
*   **Source Directory:** `03_SPECS/` (recursive listing)
    *   **Relevance:** Contains templates for feature and bugfix specifications (e.g., `features/feature_spec_template.md`) and is the target location for outputs like `documentation_index.md` and `codebase_xray_analysis.json`. Key for understanding how specific requirements are documented.

## 3. Agent Mode Definitions and Capabilities

*   **Source File:** `.roomodes`
    *   **Relevance:** This is the central file defining all AI agent modes, their `roleDefinition`, and `customInstructions`. It is the primary target for modification and integration efforts. Understanding its current structure and content is paramount.

## 4. Supporting Configuration and State (for context)

*   **Source File (Conceptual):** `project_session_state.json` (as described in `01_AI-RUN/02_AutoPilot.md`)
    *   **Relevance:** While the actual file content isn't provided for direct analysis in this initial research phase, its structure and intended use (managing workflow state, document paths, error states, etc.) as detailed in `02_AutoPilot.md` are critical for designing how `.roomodes` agents will interact with or replicate this state management.
*   **Source File (Conceptual):** `.swarmConfig` (mentioned in `.roomodes` for `ask-ultimate-guide-v2` and `tutorial-taskd-test-first-ai-workflow`)
    *   **Relevance:** Provides context on how the `orchestrator-pheromone-scribe` interprets natural language summaries. While not directly part of the `01_AI-RUN` workflow, understanding its role in the broader system described in `.roomodes` is useful.

## 5. General AI Search Tool (via MCP)

*   **Source:** MCP Tool (e.g., `perplexity-mcp`)
    *   **Relevance:** This tool will be used conceptually to fill knowledge gaps identified during the analysis of the provided documents, particularly if there are ambiguities or missing details regarding best practices for integrating complex, stateful workflows into agentic systems. This aligns with the "recursive self-learning approach."

The analysis of these sources will form the basis of the "Data Collection" phase of this research.