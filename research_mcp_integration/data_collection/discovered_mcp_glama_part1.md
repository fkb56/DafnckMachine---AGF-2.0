# Discovered MCP Servers from Glama.ai - Part 1

This document lists MCP servers discovered from `https://glama.ai/mcp/servers` and provides an initial assessment of their relevance to augmenting AI agentic coding capabilities.

*Last updated on source: 2025-05-15 16:20*

## Potentially Relevant MCP Servers for AI Agentic Coding:

1.  **GitHub MCP Server (`@modelcontextprotocol/github`)**
    *   **Description:** Official MCP Server for the GitHub API, enabling file operations, repository management, search functionality, and more.
    *   **Stated Capabilities:** File management, repository management, branch management, issue management, pull request management, search (code, users, issues), commit management.
    *   **Relevance to Coding:** Extremely high. Essential for any AI agent involved in code generation, modification, version control, and interacting with GitHub-hosted projects. This is likely already a core MCP for the existing workflow.
    *   **Installation (from initial prompt):** `npx -y @modelcontextprotocol/server-github`

2.  **ScreenshotOne MCP Server (`@screenshotone/mcp`)**
    *   **Description:** Allows AI assistants to capture website screenshots through the ScreenshotOne API, enabling visual context from web pages.
    *   **Relevance to Coding:** Medium. Could be useful for:
        *   Visual validation of UI changes during frontend development.
        *   Documenting visual bugs.
        *   Gathering visual context for UI/UX design tasks if an AI is involved in design analysis.
    *   **Potential Augmentation:** AI agents could be instructed to take screenshots after deploying a frontend change or when a UI test fails.

3.  **Needle MCP Server (`@needle-ai/needle-mcp`)**
    *   **Description:** Allows users to manage documents and perform Claude-powered searches using Needle through the Claude Desktop application.
    *   **Relevance to Coding:** Medium to High. If "documents" include technical specifications, code documentation, or project-related text files, this could be very useful for AI agents to search and retrieve specific information from a project's knowledge base.
    *   **Potential Augmentation:** AI agents could use this to find relevant information within project docs before attempting a coding task, similar to how `context7` is used for public library docs.

4.  **hostinger-api-mcp (`@hostinger/api-mcp-server`)**
    *   **Description:** Enables seamless integration of Hostinger’s API with AI tools, allowing AI models to fetch live data or perform real-time actions on hosting infrastructure.
    *   **Relevance to Coding:** Medium. Primarily for DevOps and deployment automation.
    *   **Potential Augmentation:** AI agents involved in deployment (like **DeployMaster**) could use this to manage Hostinger-based infrastructure.

5.  **EdgeOne Pages MCP (`@TencentEdgeOne/edgeone-pages-mcp`)**
    *   **Description:** Enables rapid deployment of HTML content to EdgeOne Pages and automatically generates publicly accessible URLs.
    *   **Relevance to Coding:** Medium. Specific to deploying static HTML content to Tencent EdgeOne.
    *   **Potential Augmentation:** Could be used by AI agents for quick previews of static sites or HTML-based components.

6.  **Genkit MCP (`@firebase/genkit`)**
    *   **Description:** Provides integration between Genkit (an open-source framework for building AI-powered applications) and MCP.
    *   **Relevance to Coding:** High. If the project involves building AI features or using Genkit, this MCP would be essential for AI agents to interact with and manage Genkit flows.
    *   **Potential Augmentation:** AI agents could build, test, and deploy Genkit flows.

7.  **Textin MCP Server (`@intsig-textin/textin-mcp`)**
    *   **Description:** Enables OCR capabilities to recognize text from images, PDFs, and Word documents, convert them to Markdown, and extract key information.
    *   **Relevance to Coding:** Low to Medium. Could be useful if coding tasks involve processing information from such documents (e.g., extracting requirements from a PDF spec not available in other formats).
    *   **Potential Augmentation:** AI agents could use this to make non-machine-readable documents accessible for further processing.

8.  **vizro-mcp (`@mckinsey/vizro`)**
    *   **Description:** (No detailed description, just "vizro-mcp"). Vizro is a toolkit for creating Python data visualization applications.
    *   **Relevance to Coding:** Medium. If the project involves data visualization tasks using Python.
    *   **Potential Augmentation:** AI agents could generate or modify Vizro dashboards.

9.  **DataForSEO MCP Server (`@dataforseo/mcp-server-typescript`)**
    *   **Description:** Enables Claude to interact with DataForSEO APIs (SERPs, keyword research, on-page metrics, domain analytics).
    *   **Relevance to Coding:** Low. Primarily for SEO and marketing tasks. Might be relevant if the coding task involves building SEO-related features.

10. **Aiven MCP Server (`@Aiven-Open/mcp-aiven`)**
    *   **Description:** Provides access to Aiven services (PostgreSQL, Kafka, ClickHouse, Valkey, OpenSearch), enabling LLMs to build full stack solutions.
    *   **Relevance to Coding:** High. If using Aiven-managed services for backend infrastructure.
    *   **Potential Augmentation:** AI agents could manage databases, message queues, and search indexes on Aiven.

11. **dbt-mcp (`@dbt-labs/dbt-mcp`)**
    *   **Description:** (No detailed description, just "dbt-mcp"). dbt (data build tool) is a transformation workflow tool.
    *   **Relevance to Coding:** Medium to High. If the project uses dbt for data transformation.
    *   **Potential Augmentation:** AI agents could manage dbt models, run transformations, and test data pipelines.

12. **DeepL MCP Server (`@DeepLcom/deepl-mcp-server`)**
    *   **Description:** Enables AI assistants to translate and rephrase text using the DeepL API.
    *   **Relevance to Coding:** Low. Primarily for localization or content tasks. Might be relevant if coding involves internationalization features.

13. **Sanity MCP Server (`@sanity-io/sanity-mcp-server`)**
    *   **Description:** Connects Sanity (headless CMS) content to AI agents. Allows creating, updating, and exploring structured content.
    *   **Relevance to Coding:** Medium to High. If the project uses Sanity as a CMS.
    *   **Potential Augmentation:** AI agents could manage content, generate content schemas, or integrate Sanity content into applications.

14. **mcp-server-browserbase (`@browserbase/mcp-server-browserbase`)**
    *   **Description:** Provides cloud browser automation capabilities using Browserbase, Puppeteer, and Stagehand. Enables LLMs to interact with web pages, take screenshots, and execute JavaScript.
    *   **Relevance to Coding:** High. Very useful for:
        *   End-to-end testing of web applications.
        *   Scraping dynamic websites for information needed during development.
        *   Automating UI interactions for testing or data gathering.
    *   **Potential Augmentation:** AI agents could write and execute browser automation scripts for testing or information retrieval. This complements the existing Puppeteer MCP.

15. **e2b-mcp-server (`@e2b-dev/mcp-server`)**
    *   **Description:** Using MCP to run code via e2b (custom sandboxed cloud environments for AI agents).
    *   **Relevance to Coding:** Very High. This allows AI agents to safely execute code, install dependencies, and interact with a file system in a sandboxed environment.
    *   **Potential Augmentation:** Could be a core tool for AI agents to perform complex coding tasks, test snippets, or even run parts of the build process.

16. **YDB MCP (`@ydb-platform/ydb-mcp`)**
    *   **Description:** MCP server for YDB databases, enabling AI-powered database operations and natural language interactions.
    *   **Relevance to Coding:** Medium to High. If YDB is the chosen database.
    *   **Potential Augmentation:** AI agents could manage schema, query data, and perform other database operations on YDB.

17. **NEAR MCP (`@nearai/near-mcp`)**
    *   **Description:** Interact with the NEAR blockchain through MCP calls.
    *   **Relevance to Coding:** Niche. Only if the project involves NEAR blockchain development.

18. **Alibaba Cloud MCP Server (`@aliyun/alibabacloud-ecs-mcp-server`)**
    *   **Description:** Enables management of Alibaba Cloud ECS resources.
    *   **Relevance to Coding:** Medium. For DevOps and deployment if using Alibaba Cloud.

19. **ElevenLabs MCP Server (`@elevenlabs/elevenlabs-mcp`)**
    *   **Description:** Enables AI clients to interact with ElevenLabs' Text to Speech and audio processing APIs.
    *   **Relevance to Coding:** Low. Specific to audio generation/processing features. This is already known to the project.

20. **mcp-server-circleci (`@CircleCI-Public/mcp-server-circleci`)**
    *   **Description:** Lets MCP clients use natural language to accomplish things with CircleCI (e.g., find failed pipelines, get logs).
    *   **Relevance to Coding:** Medium to High. For CI/CD pipeline management and monitoring.
    *   **Potential Augmentation:** AI agents could interact with CircleCI to check build statuses, retrieve logs for debugging, or trigger pipelines.

21. **Astra DB MCP Server (`@datastax/astra-db-mcp`)**
    *   **Description:** Allows LLMs to interact with Astra DB databases (Cassandra-as-a-service).
    *   **Relevance to Coding:** Medium to High. If Astra DB is used.
    *   **Potential Augmentation:** AI agents could manage collections and records in Astra DB.

22. **Doris MCP Server (`@apache/doris-mcp-server`)**
    *   **Description:** Connects to Apache Doris databases, allowing SQL queries, metadata management, and potentially NL to SQL.
    *   **Relevance to Coding:** Medium to High. If Apache Doris is used.

*(This list is based on the initially visible servers from the scrape. More might be available via "Load More" on the actual page.)*

This initial pass identifies several MCPs with strong potential for augmenting coding tasks, especially those related to cloud infrastructure management (Hostinger, Aiven, Alibaba), specialized databases (YDB, Astra DB, Doris), CI/CD (CircleCI), code execution sandboxes (e2b), and advanced browser automation (Browserbase). The GitHub MCP is foundational.