# Executive Summary: Integrating AI-RUN Workflows into `.roomodes`

This research investigated the integration of the comprehensive project development workflows detailed in `01_AI-RUN`, `02_AI-DOCS`, and `03_SPECS` into the existing agent capabilities defined in the `.roomodes` file. The goal was to enable `.roomodes` agents to understand, execute, and leverage these structured workflows, thereby enhancing their ability to manage and implement complex software projects from idea to deployment.

**Key Findings & Analysis:**

The `01_AI-RUN` workflow, orchestrated by `02_AutoPilot.md`, presents a detailed, state-driven, multi-phase process. Key characteristics include granular state tracking via `project_session_state.json`, dynamic persona adoption, a "template-to-instance" document generation pattern for `02_AI-DOCS` and `03_SPECS`, explicit user validation points, and prescribed MCP tool usage for specific tasks (e.g., `context7` for documentation, `shadcn` for UI components). A strong emphasis is placed on UI/UX quality, guided by foundational principles.

The existing `.roomodes` framework operates on a different paradigm, with agents having fixed personas and a more global state managed via `.pheromone` signals and a documentation registry. Direct, full replication of the `01_AI-RUN` state and persona mechanisms within `.roomodes` presents significant challenges.

**Proposed Integrated Model & Recommendations:**

A hybrid approach is recommended, focusing on augmenting existing `.roomodes` agents:

1.  **Orchestration:** The `uber-orchestrator` (or a new, dedicated "AI-RUN Workflow Orchestrator") should manage the overall sequence of `01_AI-RUN` phases.
2.  **State Management:**
    *   Major phase completions and key document paths from the `01_AI-RUN` workflow should be signaled and tracked via `.pheromone`'s `documentation_registry`.
    *   Granular, in-phase state can be managed internally by the `.roomodes` agent responsible for that phase, or by breaking complex phases into smaller, sequentially delegated tasks.
3.  **Persona Alignment:** `01_AI-RUN` phases should be mapped to existing `.roomodes` agents with the best-fit fixed personas. Phase-specific logic will be embedded in their `customInstructions`.
4.  **Document Generation:** The "template-to-instance" logic must be explicitly added to the `customInstructions` of relevant `.roomodes` document-creating agents.
5.  **MCP Tool Usage:** Prescribed MCP usage patterns from `01_AI-RUN` must be explicitly scripted into the `customInstructions` of relevant worker modes.
6.  **UI/UX Focus:** Directives to consult and apply foundational UI/UX principles (from `02_AI-DOCS/Documentation/`) must be added to the `customInstructions` of design-related modes.
7.  **User Validation:** Mandatory validation points can be handled using the `ask_followup_question` tool by the relevant `.roomodes` agent.

**Practical Application:**

The integration will enable `.roomodes` agents to execute a highly structured, end-to-end project development lifecycle. This involves:
*   The `uber-orchestrator` initiating the `01_AI-RUN` workflow.
*   Delegating phases (e.g., Market Research, PRD Generation, Specs & Docs, Implementation, Testing, Deployment) to appropriately augmented existing `.roomodes` agents like `research-planner-strategic`, `spec-writer-feature-overview`, `coder-test-driven`, `tester-tdd-master`, and `devops-pipeline-manager`.
*   These agents will follow the specific logic, document creation patterns (including template copying), and MCP usage detailed in the `01_AI-RUN` sub-prompts, guided by their updated `customInstructions`.

**Conclusion:**

Integrating the `01_AI-RUN`, `02_AI-DOCS`, and `03_SPECS` workflows into `.roomodes` is feasible through targeted augmentation of existing agent instructions and a pragmatic approach to state management. This will significantly enhance the swarm's capability to autonomously manage and execute complex projects with a strong emphasis on structured documentation, UI/UX quality, and adherence to a defined lifecycle. The detailed recommendations in this report provide a roadmap for these modifications, respecting the user's preference for targeted changes.