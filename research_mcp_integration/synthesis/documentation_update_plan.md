# Plan for Updating `01_AI-RUN` and `02_AI-DOCS` Documentation

This document outlines the specific updates required for the `01_AI-RUN/` workflow prompts and `02_AI-DOCS/` documentation to reflect the integration of new MCP servers and enhanced MCP installation/management procedures.

## I. Updates to `01_AI-RUN/` Workflow Prompts

The goal is to ensure AI personas are aware of and correctly utilize the enhanced MCP ecosystem.

1.  **[`01_AI-RUN/01_Getting_Started.md`](../../../01_AI-RUN/01_Getting_Started.md)**
    *   **Section: AI Agent Initial Onboarding / How to Use This Workflow / Project Setup**
        *   Add a new sub-section or integrate into existing setup steps: "Setting Up Your MCP Environment."
        *   Instruct the user to run the new `scripts/setup_mcps.sh` script (to be created based on research).
        *   Explain the `.env` file convention for API keys and direct them to the `.env.example` file.
        *   Mention the possibility of an "MCP Health Check" script/tool.
    *   **Section: AI Agent Initial Onboarding / Analyze File Structure**
        *   Add `scripts/` to the list of key directories if the `setup_mcps.sh` script is placed there.
    *   **Rationale:** Provides users with the new, streamlined process for MCP setup.

2.  **[`01_AI-RUN/02_AutoPilot.md`](../../../01_AI-RUN/02_AutoPilot.md)**
    *   **Section: Core Operational Rules**
        *   Add a new rule: "**MCP Ecosystem Awareness & Prioritization**".
            *   ProjectArchitect AI should be aware of all MCPs defined in [`MCP-Server.json`](../../../01_AI-RUN/Template/MCP-Server.json).
            *   When a sub-prompt's task could benefit from an MCP (e.g., code execution, documentation lookup, UI generation, file system access, version control), ProjectArchitect should ensure the sub-persona is guided to use the most appropriate available MCP.
            *   This includes prioritizing `context7` for library docs, `e2b-dev/mcp-server` or similar for code execution, memory MCPs for context, GitHub MCP for repo interactions, `shadcn` / `@21st-dev/magic` for UI, etc.
            *   If an MCP requires an API key not yet configured (based on a conceptual check or feedback from a failed MCP tool use), ProjectArchitect should guide the user to update their `.env` file.
    *   **Section: General Phase Structure / Prerequisite Document & Tool Check**
        *   Expand the "(Conceptual) For phases requiring external tools (e.g., MCPs, git)" point.
        *   ProjectArchitect should conceptually verify that key MCPs expected for a phase (e.g., GitHub MCP for implementation, `context7` for specs & docs) are listed in [`MCP-Server.json`](../../../01_AI-RUN/Template/MCP-Server.json) and that the setup script/guide has been mentioned to the user.
    *   **Rationale:** Ensures the orchestrating AI is actively considering and guiding the use of the full MCP suite.

3.  **[`01_AI-RUN/07_Specs_Docs.md`](../../../01_AI-RUN/07_Specs_Docs.md) (TechDocNavigator)**
    *   **Section: Phase 2: Documentation Gathering / Automated Collection**
        *   *Existing updates for `context7`, `shadcn`, `@21st-dev/magic` are good.*
        *   Add a general statement: "For any other specialized tasks (e.g., interacting with specific cloud services like AWS/Azure, databases like PostgreSQL/MongoDB, CI/CD like CircleCI, code analysis like Snyk/Codacy, or advanced RAG with vector databases like Pinecone/Chroma), consult the project's [`MCP-Server.json`](../../../01_AI-RUN/Template/MCP-Server.json) and the `MCP_Management_Guide.md` (in `02_AI-DOCS/Deployment/`) to identify and utilize relevant MCPs. Prioritize official and well-documented MCPs."
    *   **Section: Phase 3: Knowledge Organization / Documentation Processing for Creation**
        *   When populating `02_AI-DOCS/Conventions/coding_conventions.md`, add a sub-section on "Utilizing Code Analysis & Security MCPs" (e.g., Snyk, Codacy) and how their findings should be incorporated.
    *   **Rationale:** Makes TechDocNavigator aware of a broader range of available tools beyond the explicitly listed ones.

4.  **[`01_AI-RUN/08_Start_Building.md`](../../../01_AI-RUN/08_Start_Building.md) (ImplementationArchitect)**
    *   **Section: Implementation Process (for each task)**
        *   After "Consult `context7`...", add: "**Utilize Code Execution/Sandboxing MCPs:** For tasks requiring code execution, testing snippets, or isolated environment interactions, use appropriate MCPs like `@e2b-dev/mcp-server` or a similar configured code sandbox. Refer to `MCP_Management_Guide.md` for details."
        *   Add: "**Leverage Memory MCPs:** For complex tasks or to maintain context across multiple steps, query and update the project's memory MCP (e.g., `@modelcontextprotocol/server-memory` or a configured Knowledge Graph MCP) as appropriate."
    *   **Section: MCP Utilization**
        *   *Existing updates for `context7`, `shadcn`, `@21st-dev/magic` are good.*
        *   Add a new point: "**Code Execution & Sandboxing:**"
            *   "Utilize `@e2b-dev/mcp-server` (or equivalent configured sandbox) for running and testing code snippets, dependency installation tests, or any task requiring isolated code execution."
            *   "Ensure all code execution adheres to security best practices outlined in `coding_conventions.md`."
        *   Add a new point: "**Code Analysis & Security:**"
            *   "Optionally, or when specified by the task, use MCPs like Codacy or Snyk (if configured) to scan generated code for quality issues and vulnerabilities. Report findings as per project guidelines."
        *   Add a new point: "**IDE/Filesystem Interaction:**"
            *   "For direct file manipulations beyond simple writes (if more efficient than standard tools) or for interacting with the local IDE (if an MCP like `@block/code-mcp` is configured), refer to their specific documentation. Always seek user confirmation for potentially destructive actions."
    *   **Rationale:** Equips ImplementationArchitect with more powerful tools for coding, testing, and maintaining context.

## II. Updates to `02_AI-DOCS/` Documentation

1.  **New File: `02_AI-DOCS/Deployment/MCP_Management_Guide.md`**
    *   **Purpose:** A comprehensive guide for users and AI agents on setting up, configuring, managing, and troubleshooting MCP servers for the project.
    *   **Content Outline:**
        *   **Introduction to MCPs in this Project:**
            *   Brief overview of MCPs and their role in the workflow.
            *   Link to the project's [`MCP-Server.json`](../../../01_AI-RUN/Template/MCP-Server.json).
        *   **Initial Setup:**
            *   Installing Node.js/npm and `uv`.
            *   Running the `scripts/setup_mcps.sh` script.
            *   Understanding and using the `.env` and `.env.example` files for API keys.
            *   How to verify MCP installations (mentioning the health check tool/script idea).
        *   **Managing API Keys and Environment Variables:**
            *   Best practices for security.
            *   Where to find API keys for common services.
        *   **Detailed Guide for Key MCP Categories:**
            *   **Core MCPs (GitHub, Context7, Filesystem, Memory, Code Execution/Sandbox):** Detailed setup, common tools, example usage, troubleshooting.
            *   **UI/Design MCPs (Shadcn, @21st-dev/magic):** Setup, how to use their tools for design and component generation, linking to `design_conventions.md`.
            *   **Cloud Service MCPs (AWS, Azure, Railway, Supabase, etc., if adopted):** Specific setup, authentication, common use cases.
            *   **Database MCPs (PostgreSQL, MongoDB, etc., if adopted):** Setup, connection strings, example queries.
            *   **Code Analysis & Security MCPs (Snyk, Codacy, if adopted):** Setup, how to run scans, interpreting results.
            *   **Other Notable MCPs:** Brief on others included in [`MCP-Server.json`](../../../01_AI-RUN/Template/MCP-Server.json).
        *   **Adding a New MCP Server:**
            *   Steps to manually add an entry to [`MCP-Server.json`](../../../01_AI-RUN/Template/MCP-Server.json).
            *   How to update the `scripts/setup_mcps.sh` if necessary.
            *   Guidance on API key management for the new MCP.
        *   **Troubleshooting Common MCP Issues:**
            *   Installation failures.
            *   API key errors.
            *   Server not starting/responding.
        *   **Managing Local MCP Server Processes (if applicable):**
            *   Guidance on using `pm2` or Docker for persistent local servers.
    *   **Rationale:** Centralizes all MCP-related information for easy reference and maintainability.

2.  **Update: [`02_AI-DOCS/Documentation/AI_Coding_Agent_Optimization.md`](../../../02_AI-DOCS/Documentation/AI_Coding_Agent_Optimization.md)**
    *   Add a section: "Leveraging MCPs for Enhanced Coding."
        *   Discuss how to effectively use `context7` for accurate API info.
        *   Explain the benefits and usage patterns for code execution/sandboxing MCPs (e.g., testing generated functions).
        *   Mention using memory MCPs to recall coding patterns or project-specific architectural decisions.
        *   Refer to the main `MCP_Management_Guide.md` for setup details.
    *   **Rationale:** Provides specific advice to AI coding personas.

3.  **Update: [`02_AI-DOCS/Documentation/AI_Design_Agent_Optimization.md`](../../../02_AI-DOCS/Documentation/AI_Design_Agent_Optimization.md)**
    *   Add a section: "Utilizing Design-Focused MCPs."
        *   Detail how to use `shadcn` MCP for installing and understanding Shadcn/UI components.
        *   Explain how to use `@21st-dev/magic` for component inspiration, generation (`21st_magic_component_builder`), and logo search.
        *   Emphasize aligning outputs with `design_conventions.md`.
        *   Refer to the main `MCP_Management_Guide.md` for setup.
    *   **Rationale:** Guides AI design personas in using specialized UI/UX tools.

4.  **Update: [`02_AI-DOCS/Conventions/design_conventions.md`](../../../02_AI-DOCS/Conventions/design_conventions.md) (This file is created from a template)**
    *   When this file is populated by the **TechDocNavigator** (as per `07_Specs_Docs.md`), ensure it includes:
        *   Specific guidance on how components from `shadcn` or those inspired/generated by `@21st-dev/magic` should be themed or customized to fit the project's overall aesthetic.
        *   References to any specific UI libraries or design systems whose documentation might be fetched via `context7`.
    *   **Rationale:** Ensures consistency when using MCP-generated UI assets.

5.  **Update: [`02_AI-DOCS/TaskManagement/Roo_Task_Workflow.md`](../../../02_AI-DOCS/TaskManagement/Roo_Task_Workflow.md)**
    *   In sections describing task decomposition or detail generation, add a note that tasks involving specific libraries or external services should prompt the implementing agent to consult relevant MCPs (like `context7` for docs, or service-specific MCPs for interaction).
    *   **Rationale:** Ensures task details implicitly guide towards MCP usage.

This plan provides a roadmap for documenting the enhanced MCP ecosystem and integrating its usage into the AI agent workflow.