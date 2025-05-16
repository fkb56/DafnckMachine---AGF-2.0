# Research Scope Definition: Integrating AI-RUN, AI-DOCS, and SPECS Workflows into .roomodes

## 1. Research Objective

The primary objective of this research is to develop a comprehensive plan for integrating the workflows, processes, and logic detailed in the `01_AI-RUN`, `02_AI-DOCS`, and `03_SPECS` documentation sets into the operational capabilities of the AI agent modes defined in the `.roomodes` file. This integration aims to ensure the agent can understand, execute, and leverage these workflows effectively across its various operational modes, enhancing its project management and execution capabilities.

## 2. Key Areas of Investigation

The research will focus on the following key areas:

*   **Workflow Analysis:**
    *   Detailed deconstruction of the `01_AI-RUN` workflow, including its phases (e.g., Getting Started, Idea, Market Research, PRD Generation, Specs & Docs, Task Manager, Start Building, Testing, Deployment), state management (`project_session_state.json`), error handling, persona management, and interaction points.
    *   Understanding the structure, purpose, and lifecycle of documents and templates within `02_AI-DOCS` (e.g., architecture, conventions, AI guidance) and `03_SPECS` (e.g., feature/bugfix specifications, `documentation_index.md`, `codebase_xray_analysis.json`).
    *   Identifying the "template-to-instance" pattern where project-specific documents are created from templates in `02_AI-DOCS` and `03_SPECS`.
*   **`.roomodes` Agent Capability Mapping:**
    *   Analysis of existing agent modes in `.roomodes` (e.g., `uber-orchestrator`, `orchestrator-sparc-specification-master-test-plan`, `coder-test-driven`, `spec-writer-feature-overview`) to determine their current roles and capabilities.
    *   Identifying which existing modes are best suited to take on responsibilities outlined in the `01_AI-RUN`, `02_AI-DOCS`, and `03_SPECS` workflows.
*   **Integration Strategy:**
    *   Defining how the state-driven, sequential logic of `01_AI-RUN` (particularly `02_AutoPilot.md`) can be incorporated into the decision-making processes of relevant orchestrator modes in `.roomodes`.
    *   Specifying how agent modes should handle the creation, management, and utilization of project-specific documents derived from `02_AI-DOCS` and `03_SPECS` templates.
    *   Detailing necessary modifications to `roleDefinition` and `customInstructions` for existing modes in `.roomodes` to enable seamless workflow execution. This includes incorporating persona management, specific MCP tool usage (e.g., `context7`), and adherence to defined operational rules from `02_AutoPilot.md`.
*   **Documentation and Reporting:**
    *   Structuring the research findings into a clear, actionable report that human programmers or other AI agents can use to implement the proposed changes to `.roomodes`.
    *   Ensuring all research documentation adheres to the specified line limits per file, splitting content as necessary.

## 3. Deliverables

The primary deliverables of this research will be:

*   A structured set of research documents within the `research_workflow_integration/` directory, covering:
    *   Initial Queries (Scope, Key Questions, Information Sources)
    *   Data Collection (Analysis of `01_AI-RUN`, `02_AI-DOCS`, `03_SPECS`, and `.roomodes`)
    *   Analysis (Integration Points, Knowledge Gaps, Contradictions)
    *   Synthesis (Proposed `.roomodes` Modifications, Integration Strategy)
    *   Final Report (Executive Summary, Methodology, Detailed Findings, Recommendations)
*   A final natural language summary report detailing the research process, key findings, and the proposed integration plan, suitable for informing the SPARC Specification phase.

## 4. Constraints and Assumptions

*   The research will be based solely on the provided file contents for `01_AI-RUN`, `02_AI-DOCS`, `03_SPECS`, and `.roomodes`. No external live search will be performed beyond the conceptual use of AI search tools as described in the persona.
*   Modifications to `.roomodes` should aim to augment existing modes rather than requiring a complete overhaul, where possible, respecting the user's preference for targeted changes.
*   The integration should maintain the agent's ability to perform its existing SPARC-based tasks, with the new workflows acting as an alternative or complementary operational model.
*   A line limit of approximately 300 lines per physical Markdown file will be observed for all research documentation.

## 5. Out of Scope

*   Actual implementation of changes to the `.roomodes` file. This research provides the plan for such changes.
*   Creation of new agent modes unless deemed absolutely essential and no existing mode can be adapted.
*   Testing the integrated workflows post-modification.