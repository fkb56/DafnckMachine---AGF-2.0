# References: MCP Integration and Installation Enhancement Research

This document compiles key references used during the research into MCP integration and installation enhancements.

## Primary MCP Discovery Sources:

*   **Glama.ai MCP Server List:** `https://glama.ai/mcp/servers`
    *   (Scraped content documented in [`../data_collection/discovered_mcp_glama_part1.md`](../data_collection/discovered_mcp_glama_part1.md))
*   **Smithery.ai MCP Registry:** `https://smithery.ai/`
    *   (Scraped content documented in [`../data_collection/discovered_mcp_smithery_part1.md`](../data_collection/discovered_mcp_smithery_part1.md))
*   **Model Context Protocol GitHub - Servers Repository:** `https://github.com/modelcontextprotocol/servers`
    *   (Scraped content documented in [`../data_collection/discovered_mcp_github_part1.md`](../data_collection/discovered_mcp_github_part1.md))

## Project-Internal Context Files:

*   **Current MCP Server Definitions:** [`01_AI-RUN/Template/MCP-Server.json`](../../../01_AI-RUN/Template/MCP-Server.json)
*   **Current MCP Context Documentation:** [`01_AI-RUN/Template/MCP-Context.md`](../../../01_AI-RUN/Template/MCP-Context.md)
*   **Workflow Prompt Files (Analyzed for Integration Points):**
    *   [`01_AI-RUN/01_Getting_Started.md`](../../../01_AI-RUN/01_Getting_Started.md)
    *   [`01_AI-RUN/02_AutoPilot.md`](../../../01_AI-RUN/02_AutoPilot.md)
    *   [`01_AI-RUN/07_Specs_Docs.md`](../../../01_AI-RUN/07_Specs_Docs.md)
    *   [`01_AI-RUN/08_Start_Building.md`](../../../01_AI-RUN/08_Start_Building.md)
*   **Documentation Structure Overview:** `02_AI-DOCS/` directory structure and existing documentation templates/guides.

## Research on CLI Tool Automation and Best Practices:

*   **Perplexity AI Web Search Results (Query: "Automate installation and configuration of npx and uvx based CLI tools for project setup. Best practices for managing multiple CLI tool dependencies and their API keys in a development project.")**
    *   (Summarized findings documented in [`../data_collection/installation_automation_research.md`](../data_collection/installation_automation_research.md))
    *   Key concepts derived:
        *   Use of shell scripts for automation.
        *   Prerequisite checking (Node.js, uv).
        *   Standard API key management via environment variables and `.env` files.
        *   Dependency management tools (`npm`, `uv`).
    *   Cited sources from search:
        *   [https://github.com/astral-sh/uv/issues/6477](https://github.com/astral-sh/uv/issues/6477)
        *   [https://emasuriano.com/blog/2025-01-21-simplifying-python-development-with-uv-a-modern-package-management-tool/](https://emasuriano.com/blog/2025-01-21-simplifying-python-development-with-uv-a-modern-package-management-tool/)
        *   [https://docs.astral.sh/uv/getting-started/installation/](https://docs.astral.sh/uv/getting-started/installation/)
        *   [https://github.com/adhikasp/mcp-client-cli](https://github.com/adhikasp/mcp-client-cli)
        *   [https://www.productcompass.pm/p/n8n-mcp-servers-uv](https://www.productcompass.pm/p/n8n-mcp-servers-uv)

## General Tooling Documentation (Implicitly Referenced):

*   **Node.js and `npx` documentation:** For understanding `npx` behavior.
*   **Astral `uv` and `uvx` documentation:** For understanding `uvx` behavior.
*   **Shell scripting guides (Bash/Zsh):** For conceptualizing the `setup_mcps.sh` script.
*   **`dotenv` library documentation (or similar):** For the concept of loading `.env` files.
*   **`pm2` and Docker documentation:** For managing persistent local servers.

This list forms the primary basis of information used to derive the findings, analysis, and recommendations in this research report.