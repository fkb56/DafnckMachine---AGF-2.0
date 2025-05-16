# Key Research Questions: Integrating AI-RUN, AI-DOCS, and SPECS Workflows

This document outlines the key questions that will guide the research into integrating the `01_AI-RUN`, `02_AI-DOCS`, and `03_SPECS` workflows into the `.roomodes` agent definitions.

## 1. Understanding the `01_AI-RUN` Workflow

*   **Q1.1:** What are the distinct phases of the `01_AI-RUN` workflow (as detailed in `01_Getting_Started.md` and `02_AutoPilot.md`)?
*   **Q1.2:** How is state managed across these phases, particularly concerning `project_session_state.json` (e.g., `currentWorkflowPhase`, `lastCompletedStep`, `documents`, `filenameMapping`)?
*   **Q1.3:** What are the specific inputs and outputs for each phase in `01_AI-RUN`?
*   **Q1.4:** How does `02_AutoPilot.md` orchestrate the execution of sub-prompts (e.g., `03_Idea.md`, `04_Market_Research.md`)? What is the persona adoption mechanism?
*   **Q1.5:** What are the error handling and user intervention mechanisms defined in `02_AutoPilot.md`?
*   **Q1.6:** What is the "Foolproof Template Copying" mechanism described in `02_AutoPilot.md` for the "Specs & Docs" phase, and how does it relate to `02_AI-DOCS` and `03_SPECS`?
*   **Q1.7:** How does the `01_AI-RUN` workflow envision the use of MCP tools (e.g., `context7`, `github`, `firecrawl`, `shadcn`, `@21st-dev/magic`)?
*   **Q1.8:** What is the role and significance of the "In-Depth Codebase Understanding" (Codebase Xray) step mentioned in `01_Getting_Started.md` and its output (`03_SPECS/codebase_xray_analysis.json`)?

## 2. Understanding `02_AI-DOCS` and `03_SPECS` Structures and Content

*   **Q2.1:** What is the overall purpose and structure of the `02_AI-DOCS` directory and its subdirectories (e.g., `Architecture`, `Conventions`, `Documentation`, `TaskManagement`)?
*   **Q2.2:** What is the nature of the template files within `02_AI-DOCS` (e.g., `architecture_template.md`, `coding_conventions_template.md`, `design_conventions_template.md`)?
*   **Q2.3:** How are project-specific documents intended to be created and populated from these templates (e.g., `architecture.md` from `architecture_template.md`)?
*   **Q2.4:** What is the role of foundational documents like `AI_Design_Agent_Optimization.md` and `AI_Coding_Agent_Optimization.md` in guiding the population of project-specific convention documents?
*   **Q2.5:** What is the purpose and structure of the `03_SPECS` directory and its subdirectories (e.g., `features`, `bugfixes`)?
*   **Q2.6:** How are feature and bugfix specifications (e.g., `feature_spec_FEAT-XXX.md`) generated and used?
*   **Q2.7:** What is the role of `03_SPECS/documentation_index.md`?

## 3. Analyzing `.roomodes` Agent Capabilities

*   **Q3.1:** What are the current `roleDefinition` and `customInstructions` for each key orchestrator and worker mode in `.roomodes` (e.g., `uber-orchestrator`, `orchestrator-sparc-specification-master-test-plan`, `research-planner-strategic`, `spec-writer-feature-overview`, `coder-test-driven`)?
*   **Q3.2:** Which existing modes in `.roomodes` have responsibilities that align with the phases or tasks described in the `01_AI-RUN` workflow?
*   **Q3.3:** How do current modes handle state, document creation/management, and MCP tool usage?
*   **Q3.4:** Are there any existing mechanisms in `.roomodes` for persona adoption or sequential task execution similar to `02_AutoPilot.md`?

## 4. Integration Strategy and `.roomodes` Modification

*   **Q4.1:** How can the state-driven logic of `02_AutoPilot.md` (using `project_session_state.json`) be integrated into the decision-making of relevant `.roomodes` orchestrators?
*   **Q4.2:** Which specific `roleDefinition` and `customInstructions` in `.roomodes` need modification to incorporate the `01_AI-RUN` workflow logic?
*   **Q4.3:** How should agent modes be instructed to handle the "template-to-instance" creation of documents in `02_AI-DOCS` and `03_SPECS`?
*   **Q4.4:** How can the persona management concept from `01_AI-RUN` be mapped to or adopted by `.roomodes` agents?
*   **Q4.5:** What specific instructions are needed for `.roomodes` agents regarding the use of MCPs like `context7`, `shadcn`, `@21st-dev/magic` as outlined in `01_AI-RUN` (e.g., in `07_Specs_Docs.md` and `08_Start_Building.md`)?
*   **Q4.6:** How should the "In-Depth Codebase Understanding" (Codebase Xray) step and its output be integrated into the operational flow of relevant `.roomodes` agents?
*   **Q4.7:** What are the precise line numbers or regex patterns in `.roomodes` that are candidates for modification to achieve this integration, aligning with the user's preference for targeted changes?
*   **Q4.8:** How can the agent ensure that the "Structured Summary of UI/UX Principles" (derived from `02_AI-DOCS/Documentation/`) is consistently applied when generating design-related documents and specifications, as emphasized in `07_Specs_Docs.md`?
*   **Q4.9:** What mechanisms are needed to ensure the agent correctly identifies and uses project-specific generated documents (e.g., `02_AI-DOCS/Conventions/design_conventions.md`) over the original templates?

## 5. Output and Reporting

*   **Q5.1:** How can the research findings be structured to provide a clear and actionable plan for modifying `.roomodes`?
*   **Q5.2:** What is the most effective way to present the proposed changes to `.roomodes` (e.g., diffs, narrative descriptions of changes per mode)?
*   **Q5.3:** How can the final report effectively communicate the integration strategy to human programmers and AI orchestrators?

These questions will be refined and expanded as the research progresses.