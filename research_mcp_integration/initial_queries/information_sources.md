# Information Sources for MCP Integration and Installation Enhancement Research

This document lists the primary sources of information that will be consulted for researching new MCP servers, evaluating their potential, and enhancing MCP installation/management within the project.

## 1. MCP Discovery Sources

*   **`https://glama.ai/mcp/servers`**: This will be a primary source for discovering existing MCP servers, their capabilities, and installation commands.
*   **`https://smithery.ai/`**: This site will be investigated for any direct MCP server offerings or for compatible tools/technologies that could be relevant to AI agentic coding and potentially wrapped as MCPs. The focus will be on identifying technologies that augment coding or development workflows.
*   **`https://github.com/modelcontextprotocol/servers`**: The official/community GitHub organization for MCP servers will be explored for additional, perhaps newer or more experimental, MCPs. READMEs and repository content will be key.
*   **General AI Search Tool (via Perplexity AI MCP Tool):** For any promising MCPs or technologies found, further web searches will be conducted to find:
    *   Official documentation.
    *   GitHub repositories (if not already found).
    *   Tutorials, blog posts, and community discussions.
    *   Use cases and examples.

## 2. MCP Evaluation and Installation Enhancement Sources

*   **Discovered MCP Documentation:** Official documentation, READMEs, and examples for each identified MCP will be the primary source for understanding its tools, schemas, installation process, and configuration.
*   **Existing Project Files:**
    *   [`01_AI-RUN/Template/MCP-Server.json`](../../01_AI-RUN/Template/MCP-Server.json): To understand the current method of defining MCP servers.
    *   [`01_AI-RUN/Template/MCP-Context.md`](../../01_AI-RUN/Template/MCP-Context.md): To see how MCPs are currently contextualized for the project.
    *   The list of already connected MCPs (from the initial prompt) will serve as a baseline.
*   **Node.js/npm/npx Documentation:** For understanding `npx` execution, package management, and potential scripting/automation of `npx`-based tool installations.
*   **Python/uvx/pipx Documentation:** For understanding `uvx` (if it's a pipx wrapper or similar) and Python-based tool installation and management.
*   **Shell Scripting Guides (Bash/Zsh):** For developing simple automation scripts for MCP installation and management if deemed appropriate.
*   **Process Management Tools (e.g., `pm2`, Docker):** Documentation for these tools will be consulted if they are considered for managing local MCP server instances.
*   **Security Best Practices:** General security guidelines for managing API keys and environment variables.

## 3. Workflow Integration and Documentation Update Sources

*   **Existing `01_AI-RUN/` prompt files:** These will be analyzed to identify insertion points for new MCP usage instructions and installation/management procedures.
*   **Existing `02_AI-DOCS/` structure and content:** This will inform the creation of new documentation or updates to existing guides regarding MCPs.
*   **The research findings from this current task** will be the primary driver for the content of these updates.

## 4. Information Gathering Strategy

1.  **Systematic Discovery:** Visit each specified URL (`glama.ai`, `smithery.ai`, `github.com/modelcontextprotocol/servers`) and systematically list potential MCPs.
2.  **Initial Filtering:** Quickly filter the list for MCPs that seem most relevant to "AI agentic coding capabilities" (e.g., code generation, analysis, testing, advanced documentation access, UI generation).
3.  **In-Depth Research on Filtered MCPs:** For each filtered MCP, use the AI search tool and direct repository exploration to gather details on capabilities, installation, and usage.
4.  **Installation/Management Research:** Concurrently, research best practices and tools for automating or simplifying `npx` and `uvx` based tool installations and management.
5.  **Analysis and Synthesis:** Evaluate each MCP's potential, compare with existing tools, and identify optimal integration points and installation strategies.
6.  **Documentation Planning:** Outline the necessary changes and additions to `01_AI-RUN/` and `02_AI-DOCS/` based on the synthesized findings.