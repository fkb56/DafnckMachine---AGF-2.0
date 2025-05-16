# Information Sources for context7 MCP Research

This document lists the potential sources of information that will be consulted during the research on the "context7" MCP.

## 1. Primary Information Source

*   **General AI Search Tool (via MCP):** The primary method for gathering information about "context7" will be through targeted queries using an AI search tool. This will be used to find:
    *   Official documentation for "context7" (if publicly available).
    *   Developer blogs, articles, or tutorials discussing "context7".
    *   Community discussions (e.g., forums, Q&A sites) mentioning "context7".
    *   Any available examples or use cases of "context7".
    *   Information about Upstash, the likely provider of "context7" given the MCP server command `npx -y @upstash/context7-mcp@latest`.

## 2. Internal Project Resources

*   **[`01_AI-RUN/Template/MCP-Context.md`](01_AI-RUN/Template/MCP-Context.md):** This file will be examined for any existing contextual information or notes about "context7" within the project.
*   **[`01_AI-RUN/Template/MCP-Server.json`](01_AI-RUN/Template/MCP-Server.json):** This file will be checked for configuration details, tool definitions, or any other metadata related to the "context7" MCP server.
*   **MCP Server List (provided in the initial prompt):** The description of the `context7` MCP server itself, including its tools (`resolve-library-id`, `get-library-docs`) and their input schemas, will be a crucial source.

## 3. Implicit Information Sources

*   **Tool Schemas:** The input and output schemas of the `context7` tools (`resolve-library-id` and `get-library-docs`) as described in the MCP server list will provide direct insight into their functionality and data handling.
*   **MCP Server Command:** The command `npx -y @upstash/context7-mcp@latest` suggests that "context7" is related to Upstash and is an npm package. This will guide some search queries.

## 4. Information Gathering Strategy

1.  **Examine Internal Resources:** Start by thoroughly reviewing the content of [`MCP-Context.md`](01_AI-RUN/Template/MCP-Context.md) and [`MCP-Server.json`](01_AI-RUN/Template/MCP-Server.json), and the provided MCP server description for `context7`.
2.  **Targeted AI Search:**
    *   Formulate initial search queries based on "context7 MCP," "Upstash context7," "context7 resolve-library-id," and "context7 get-library-docs."
    *   Refine queries based on initial findings to delve deeper into specific features, use cases, and benefits.
    *   Specifically search for how it might provide documentation or context for various libraries and technologies relevant to the software development lifecycle stages (technical, design, frontend, backend).
3.  **Synthesize Information:** Consolidate findings from all sources, noting any discrepancies or confirmations.