# MCP Integration Strategy and Enhanced Management

This document outlines a strategy for integrating newly discovered, valuable Model Context Protocol (MCP) servers and for implementing enhancements to the overall MCP installation and management process within the project.

## Guiding Principles

*   **Augment AI Agent Capabilities:** Prioritize MCPs that directly enhance the coding, analysis, design, or automation capabilities of the AI agents in the workflow.
*   **Improve Developer Experience:** Streamline MCP setup and management to reduce friction for human developers and AI orchestrators.
*   **Maintainability:** Proposed solutions should be maintainable and clearly documented.
*   **Security:** API key management and command execution must consider security best practices.
*   **Modularity:** Allow for easy addition or removal of MCPs as project needs evolve.

## Phase 1: Implement Core Installation and Management Enhancements

This phase focuses on improving the foundational aspects of how MCPs are handled.

1.  **Develop Centralized Installation Script (`scripts/setup_mcps.sh`):**
    *   **Action:** Create the script as detailed in [`research_mcp_integration/analysis/installation_enhancements.md`](../analysis/installation_enhancements.md).
    *   **Details:**
        *   Include prerequisite checks for Node.js/npm and `uv`.
        *   Parse [`MCP-Server.json`](../../../01_AI-RUN/Template/MCP-Server.json) to iterate through defined MCPs.
        *   Attempt installation using `npx -y` or `uvx`.
        *   Provide clear instructions for manual API key setup using a `.env` file and an `.env.example` template.
    *   **Impact:** Simplifies initial setup and ensures all defined MCPs are addressed.

2.  **Establish `.env` Convention:**
    *   **Action:** Create an `.env.example` file in the project root.
    *   **Details:** This file should list all known environment variables required by MCPs (e.g., `GITHUB_PERSONAL_ACCESS_TOKEN`, `SUPABASE_ACCESS_TOKEN`, `FIRECRAWL_API_KEY`, etc.) with placeholder values.
    *   **Documentation:** Update project setup guides to instruct users to copy `.env.example` to `.env` and fill in their actual keys. Ensure `.env` is in `.gitignore`.
    *   **Impact:** Standardizes API key management and improves security by keeping secrets out of version control.

3.  **Update `01_Getting_Started.md`:**
    *   **Action:** Modify [`01_Getting_Started.md`](../../../01_AI-RUN/01_Getting_Started.md) to include:
        *   Instructions on running the new `scripts/setup_mcps.sh` script.
        *   Guidance on the `.env` file convention for API keys.
    *   **Impact:** Provides users with a clear, updated path for setting up their MCP environment.

## Phase 2: Integrate High-Value Discovered MCPs

Based on the research (documented in `discovered_mcp_*.md` files), prioritize the integration of the following types of MCPs:

1.  **Code Execution & Sandboxing (e.g., `@e2b-dev/mcp-server`, `code-sandbox-mcp`):**
    *   **Strategy:** These are critical for enabling AI agents to safely run code, test snippets, and perform file system operations.
    *   **Integration:**
        *   Add their definitions to [`MCP-Server.json`](../../../01_AI-RUN/Template/MCP-Server.json).
        *   Update `scripts/setup_mcps.sh` to handle their installation.
        *   Modify `01_AI-RUN/08_Start_Building.md` to instruct the **ImplementationArchitect** to utilize these sandboxing MCPs for code execution tasks, especially for testing generated code or running small scripts.
        *   Update `02_AI-DOCS/Documentation/AI_Coding_Agent_Optimization.md` with best practices for using these sandboxes.
    *   **Impact:** Significantly enhances the AI's ability to perform and validate coding tasks autonomously.

2.  **Enhanced Memory & Knowledge Management (e.g., `@modelcontextprotocol/server-memory`, community Knowledge Graph MCPs, RAG-focused MCPs like Needle, Chroma, Pinecone):**
    *   **Strategy:** Provide AI agents with robust short-term and long-term memory capabilities.
    *   **Integration:**
        *   Select one or two promising memory/KG MCPs for initial integration.
        *   Add to [`MCP-Server.json`](../../../01_AI-RUN/Template/MCP-Server.json) and setup script.
        *   Update `01_AI-RUN/02_AutoPilot.md` to instruct **ProjectArchitect AI** to leverage these memory MCPs for storing key decisions, learnings, and project context across phases.
        *   Instruct personas in `07_Specs_Docs.md` and `08_Start_Building.md` to query/update the memory MCPs as relevant (e.g., storing summaries of fetched documentation, recalling previous solutions).
        *   Document usage in `02_AI-DOCS/Documentation/AI_Task_Management_Optimization.md` or a new `AI_Memory_Usage_Guide.md`.
    *   **Impact:** Improves contextual understanding, reduces redundant work, and enables more sophisticated reasoning by AI agents.

3.  **IDE & Local Development Environment Interaction (e.g., `@block/code-mcp` for VS Code, Neovim MCP, Filesystem MCP):**
    *   **Strategy:** Allow AI agents to interact more directly with the developer's local environment.
    *   **Integration:**
        *   Add to [`MCP-Server.json`](../../../01_AI-RUN/Template/MCP-Server.json) and setup script.
        *   In `01_AI-RUN/08_Start_Building.md`, guide **ImplementationArchitect** to use these for tasks like opening files, applying diffs (if the MCP supports it directly and is more efficient than current methods), or listing project files beyond the initial workspace view.
        *   **Caution:** Emphasize security and user approval for file modification actions.
    *   **Impact:** Can streamline certain development tasks and provide AI agents with more immediate environmental context.

4.  **Advanced Code Analysis & Security (e.g., Codacy MCP, Snyk MCP, CodeLogic MCP):**
    *   **Strategy:** Integrate tools that help AI agents write better, more secure code, and understand existing codebases more deeply.
    *   **Integration:**
        *   Add to [`MCP-Server.json`](../../../01_AI-RUN/Template/MCP-Server.json) and setup script.
        *   In `01_AI-RUN/08_Start_Building.md`, instruct **ImplementationArchitect** to (optionally or as part of a review step) use these MCPs to scan generated code for issues or analyze dependencies.
        *   In `01_AI-RUN/07_Specs_Docs.md`, **TechDocNavigator** could use CodeLogic to understand dependencies when creating documentation.
        *   Update `02_AI-DOCS/Conventions/coding_conventions.md` to reference these tools.
    *   **Impact:** Improves code quality, security, and maintainability.

5.  **Specialized UI/Design Augmentation (Beyond existing `shadcn` and `@21st-dev/magic`):**
    *   **Strategy:** If any newly discovered MCPs offer unique advantages for "pixel perfect modern design" (e.g., advanced visual diffing, specific design tool integration), evaluate them for inclusion.
    *   **Integration:** Similar to other MCPs: add to JSON, setup script, and update relevant prompts in `01_AI-RUN/07_Specs_Docs.md` and `01_AI-RUN/08_Start_Building.md`.
    *   **Impact:** Further enhances the AI's ability to assist with high-quality UI/UX development.

## Phase 3: Documentation and Workflow Updates

*   **Action:** Implement the changes outlined in `research_mcp_integration/synthesis/documentation_update_plan.md`.
*   **Details:** This involves updating `01_AI-RUN/` prompts to reflect new MCP capabilities and installation procedures, and creating/updating `02_AI-DOCS/` guides for comprehensive MCP management and usage.
*   **Impact:** Ensures that both human users and AI agents have clear, up-to-date information on how to use the project's MCP ecosystem.

## Iterative Approach

*   The integration of new MCPs should be iterative. Start with the highest-impact, most stable MCPs.
*   Gather feedback on their utility and ease of use.
*   Continuously monitor the MCP landscape for new tools that could benefit the project.

This strategy aims to create a more robust, efficient, and powerful MCP environment, directly supporting the goal of advanced AI agentic coding and workflow automation.