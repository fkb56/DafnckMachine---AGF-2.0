# Discovered MCP Servers from github.com/modelcontextprotocol/servers - Part 1

This document lists MCP servers discovered from the official Model Context Protocol servers GitHub repository. It focuses on servers relevant to augmenting AI agentic coding capabilities.

## Reference Servers (Maintained by MCP Core Team/Anthropic)

These servers demonstrate MCP features and SDKs. Many are highly relevant for coding tasks:

*   **Filesystem (`@modelcontextprotocol/server-filesystem`)**
    *   **Capabilities:** Secure file operations with configurable access controls.
    *   **Relevance:** Very High. Essential for AI agents needing to read, write, or manage project files.
*   **Git (`mcp-server-git` - Python, `uvx mcp-server-git`)**
    *   **Capabilities:** Tools to read, search, and manipulate Git repositories.
    *   **Relevance:** Very High. Crucial for version control, code history analysis, and automated commits/branching.
*   **GitHub (`@modelcontextprotocol/server-github`)**
    *   **Capabilities:** Repository management, file operations, GitHub API integration.
    *   **Relevance:** Foundational. Already integrated into the project workflow.
*   **GitLab (`@modelcontextprotocol/server-gitlab`)**
    *   **Capabilities:** GitLab API access, enabling project management.
    *   **Relevance:** High, if the project uses GitLab.
*   **Google Drive (`@modelcontextprotocol/server-gdrive`)**
    *   **Capabilities:** File access and search capabilities for Google Drive.
    *   **Relevance:** Medium. Useful for accessing project assets, design files, or documents stored in Google Drive.
*   **Memory (`@modelcontextprotocol/server-memory`)**
    *   **Capabilities:** Knowledge graph-based persistent memory system.
    *   **Relevance:** Very High. Enables AI agents to learn, remember context across sessions, and build a knowledge base about the project. Complements other memory solutions.
*   **PostgreSQL (`@modelcontextprotocol/server-postgres`)**
    *   **Capabilities:** Read-only database access with schema inspection for PostgreSQL.
    *   **Relevance:** High, if using PostgreSQL. Allows AI to understand database structure and query data.
*   **Puppeteer (`@modelcontextprotocol/server-puppeteer`)**
    *   **Capabilities:** Browser automation and web scraping.
    *   **Relevance:** High. Useful for E2E testing, dynamic content scraping. Already known.
*   **Redis (`@modelcontextprotocol/server-redis`)**
    *   **Capabilities:** Interact with Redis key-value stores.
    *   **Relevance:** High, if using Redis for caching or other purposes.
*   **Sentry (`@modelcontextprotocol/server-sentry`)**
    *   **Capabilities:** Retrieving and analyzing issues from Sentry.io.
    *   **Relevance:** Medium-High. Useful for AI agents involved in debugging and monitoring application health.
*   **Sequential Thinking (`@modelcontextprotocol/server-sequential-thinking`)**
    *   **Capabilities:** Dynamic and reflective problem-solving.
    *   **Relevance:** High. A general-purpose tool for complex reasoning by AI agents. Already known.
*   **Sqlite (`@modelcontextprotocol/server-sqlite`)**
    *   **Capabilities:** Database interaction and business intelligence capabilities for SQLite.
    *   **Relevance:** High, if using SQLite.

## Selected Official Third-Party Servers (Potentially Relevant for Coding)

This list highlights some official integrations from the GitHub repository that seem particularly relevant, noting overlaps with previous findings.

*   **21st.dev Magic (`@21st-dev/magic-mcp`)**: UI component creation. (Already known and integrated into workflow prompts).
*   **AgentQL (`@tinyfish-io/agentql-mcp`)**: Get structured data from unstructured web. (Medium relevance for data gathering for coding tasks).
*   **Aiven (`@Aiven-Open/mcp-aiven`)**: Manage Aiven data services (PostgreSQL, Kafka, etc.). (High if using Aiven).
*   **AWS (`@awslabs/mcp`)**: Specialized AWS best practices and service interaction. (High if using AWS).
*   **Azure (`@Azure/azure-mcp`)**: Access to Azure services. (High if using Azure).
*   **Browserbase (`@browserbase/mcp-server-browserbase`)**: Cloud browser automation. (High, complements Puppeteer).
*   **Chroma (`@chroma-core/chroma-mcp`)**: Embeddings, vector search for RAG. (High for advanced AI memory/context).
*   **Cloudflare (`@cloudflare/mcp-server-cloudflare`)**: Manage Cloudflare resources. (Medium-High for DevOps).
*   **Codacy (`@codacy/codacy-mcp-server`)**: Code quality and vulnerability analysis. (High for automated code review by AI).
*   **CodeLogic (`@CodeLogicIncEngineering/codelogic-mcp-server`)**: Graphs code/data dependencies. (High for code understanding and impact analysis by AI).
*   **Convex (`@convex-dev/convex-mcp-server`)**: Interact with Convex backend platform. (High if using Convex).
*   **E2B (`@e2b-dev/mcp-server`)**: Secure code execution sandboxes. (Very High for AI agent code execution and testing).
*   **Elasticsearch (`@elastic/mcp-server-elasticsearch`)**: Query Elasticsearch. (Relevant if used).
*   **Firecrawl (`@mendableai/firecrawl-mcp-server`)**: Advanced web scraping. (Already known).
*   **Google Cloud (via `@googleapis/genai-toolbox`)**: Database tools for AlloyDB, BigQuery, Spanner. (High if using GCP databases).
*   **Grafana (`@grafana/mcp-grafana`)**: Interact with Grafana dashboards/data. (Medium for monitoring/DevOps).
*   **JetBrains (`@JetBrains/mcp-jetbrains`)**: Interact with JetBrains IDEs. (Very High for developers using these IDEs, enabling AI-IDE interaction).
*   **Langfuse Prompt Management (`@langfuse/mcp-server-langfuse`)**: Manage and version prompts. (Medium, useful for projects heavily reliant on LLM prompts).
*   **Make (`@integromat/make-mcp-server`)**: Turn Make.com scenarios into callable tools. (Medium for workflow automation).
*   **Meilisearch (`@meilisearch/meilisearch-mcp`)**: Interact with Meilisearch search API. (Relevant if used).
*   **Memgraph (`@memgraph/mcp-memgraph`)**: Query Memgraph graph database. (Relevant if used).
*   **Milvus (`@zilliztech/mcp-server-milvus`)**: Vector database for AI applications. (High for RAG/AI memory).
*   **MongoDB (`@mongodb-js/mongodb-mcp-server`)**: Interact with MongoDB. (Already known).
*   **MotherDuck (`@motherduckdb/mcp-server-motherduck`)**: DuckDB-based analytics. (Medium for data-intensive projects).
*   **Needle (`@needle-ai/needle-mcp`)**: RAG for searching own documents. (High for project-specific knowledge retrieval).
*   **Neo4j (`@neo4j-contrib/mcp-neo4j`)**: Neo4j graph database and graph-backed memory. (High for knowledge graphs).
*   **Neon (`@neondatabase/mcp-server-neon`)**: Interact with Neon serverless Postgres. (Relevant if using Neon).
*   **Notion (`@makenotion/notion-mcp-server`)**: Interact with Notion API. (Already known).
*   **Pinecone (`@pinecone-io/pinecone-mcp`, `@pinecone-io/assistant-mcp`)**: Vector database for semantic search and RAG. (High for AI memory).
*   **Prisma (`@prisma/mcp-server-postgres` - example name)**: Manage Prisma with Postgres. (High if using Prisma).
*   **Qdrant (`@qdrant/mcp-server-qdrant`)**: Vector search engine. (High for AI memory).
*   **Redis (`@redis/mcp-redis`, `@redis/mcp-redis-cloud`)**: Interact with Redis. (Already known).
*   **Snyk (via `@snyk/snyk-ls`)**: Embed Snyk vulnerability scanning. (Very High for secure coding practices by AI).
*   **Stripe (`@stripe/agent-toolkit`)**: Interact with Stripe API. (Already known).
*   **Unstructured (`@Unstructured-IO/UNS-MCP`)**: Process unstructured data for AI. (Medium for data preparation).
*   **Vectorize (`@vectorize-io/vectorize-mcp-server`)**: RAG, file extraction, text chunking. (High for building AI context).
*   **Zapier (`zapier.com/mcp`)**: Connect to thousands of apps. (Medium for broader workflow automation).
*   **ZenML (`@zenml-io/mcp-zenml`)**: MLOps/LLMOps pipelines. (Niche, for ML-specific projects).

## Selected Community Servers (Potentially Relevant for Coding - Require Vetting)

*   **code-assistant (`@stippi/code-assistant`)**: Explore codebase, make changes. (High potential, security implications noted).
*   **code-executor (`@bazinga012/mcp_code_executor`)**: Execute Python in Conda environment. (High potential).
*   **code-sandbox-mcp (`@Automata-Labs-team/code-sandbox-mcp`)**: Secure code execution in Docker. (Very High potential).
*   **Computer-Use - Remote MacOS Use (`@baryhuang/mcp-remote-macos-use`)**: Full desktop control for agents. (High potential for complex automation).
*   **lsp-mcp (`@Tritlo/lsp-mcp`)**: Interact with Language Servers (LSP). (Very High for advanced code intelligence, completions, diagnostics for AI).
*   **Neovim (`@bigcodegen/mcp-neovim-server`)**: Interact with Neovim editor session. (High for Neovim users).
*   **Obsidian Markdown Notes (`@calclavia/mcp-obsidian`)**: Read/search Obsidian knowledge base. (High for integrating personal/team knowledge).

**Observations:**
*   This repository is a central hub for many foundational and specialized MCPs.
*   "Reference Servers" provide robust examples of core functionalities like filesystem, git, and database interactions.
*   Many "Official Third-Party Servers" offer deep integrations with popular SaaS platforms, databases, and developer tools, significantly expanding AI agent capabilities.
*   "Community Servers" show innovation, but require careful vetting for stability and security.
*   Tools for code execution (e2b, code-sandbox-mcp), IDE interaction (JetBrains, Neovim, VS Code via `@block/code-mcp` from Smithery), Language Server Protocol interaction (lsp-mcp), and advanced RAG/memory (Chroma, Milvus, Pinecone, Qdrant, Needle, Memory) are particularly promising for enhancing AI agentic coding.
*   Security tools like Snyk MCP are also highly valuable.

The next step will be to analyze the current MCP installation/management approach and research enhancements.