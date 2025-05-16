# Technical Manual: Pheromind Agentic Coding Framework - Execution Engine for 01_AI-RUN Workflows

## Introduction

This document provides an ultra-detailed technical description of the **Pheromind Agentic Coding Framework**, focusing on its internal logic and step-by-step operation. Pheromind serves as the **execution engine and state management layer** for the overarching workflow defined by the sequence of scripts within the [`01_AI-RUN/`](01_AI-RUN/) directory (e.g., [`01_AI-RUN/01_Getting_Started.md`](01_AI-RUN/01_Getting_Started.md:1), [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1)). This manual elucidates how the Pheromind swarm intelligence model, its core agents (as defined in the *newly updated* [`.roomodes`](.roomodes:1)), and key files ([`.pheromone`](.pheromone:1), [`.swarmConfig`](.swarmConfig:1)) interpret and execute these `01_AI-RUN/` scripts. The [`01_AI-RUN/`](01_AI-RUN/) scripts, particularly an entry-point like [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1), dictate the sequence of phases and the high-level logic. Pheromind agents, guided by their definitions in [`.roomodes`](.roomodes:1) and coordinated by the `🧐 @uber-orchestrator` and `✍️ @orchestrator-pheromone-scribe` (using [`.swarmConfig`](.swarmConfig:1)), carry out these instructions, driving project execution from initiation through completion and iteration, all grounded in an **AI-Verifiable Methodology**.

Pheromind leverages a collective of specialized AI agents that collaborate indirectly through a shared state medium—the [`.pheromone`](.pheromone:1) file—which is meticulously managed by the `✍️ @orchestrator-pheromone-scribe`. This framework is designed for the autonomous execution and management of complex projects, particularly software development, by carrying out the instructions and sequences defined in the [`01_AI-RUN/`](01_AI-RUN/) scripts. Progress is tracked via concrete, measurable, and AI-confirmable outcomes, ensuring alignment with the project plan dictated by files like [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1).

## Fundamental Principles of Pheromind

1.  **🧠 Pheromone-Based Swarm Intelligence (Stigmergy):**
    Agents interact indirectly by sensing and modifying a shared environment, the [`.pheromone`](.pheromone:1) file. This file contains structured JSON `:signals` (interpreted state) and a `documentationRegistry` (tracking human-readable artifacts generated during the execution of [`01_AI-RUN/`](01_AI-RUN/) workflows). The `✍️ @orchestrator-pheromone-scribe` is the sole interpreter of natural language summaries from Task Orchestrators, translating them into these "digital pheromones" that guide swarm behavior.

2.  **🎯 AI-Verifiable Project Execution Driven by [`01_AI-RUN/`](01_AI-RUN/) Scripts:**
    Project progression is **defined by the tasks and phases outlined in the [`01_AI-RUN/`](01_AI-RUN/) scripts**, each with **AI-Verifiable End Results**. The sequence and high-level logic of these tasks and phases are primarily dictated by an entry-point script like [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1). A **Master Project Plan**, often generated as an early output of executing these scripts (e.g., via [`01_AI-RUN/09_Task_Manager.md`](01_AI-RUN/09_Task_Manager.md:1)), further details phases and micro-tasks, each with specific, programmatically checkable completion criteria. This makes progress unambiguous and AI-auditable, with Pheromind agents directly executing these scripted instructions.

3.  **⚙️ Autonomous Task Orchestration based on [`01_AI-RUN/`](01_AI-RUN/) Directives and [`.roomodes`](.roomodes:1):**
    Post-initiation, Pheromind autonomously executes the project workflow as defined in the [`01_AI-RUN/`](01_AI-RUN/) scripts. The `🧐 @uber-orchestrator`, using an `01_AI-RUN/` script (e.g., [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1) specified in the `Original_User_Directive_Payload_Path_Field`) as its primary guide and its "01_AI-RUN Workflow Orchestration" logic from [`.roomodes`](.roomodes:1), delegates phases. This delegation involves identifying the next `01_AI-RUN/*.md` sub-prompt based on the current [`.pheromone`](.pheromone:1) state (last completed `01_AI-RUN` phase) and the sequence in the guiding `01_AI-RUN/` script. It then tasks the appropriate specialized Pheromind agents (defined in [`.roomodes`](.roomodes:1), e.g., `code-comprehension-assistant-v2`, `research-planner-strategic`) with executing these sub-prompts. Progress is reported via natural language summaries, interpreted by the Scribe to update the global state in [`.pheromone`](.pheromone:1). The `🧐 @uber-orchestrator` also handles user responses from `ask_followup_question` if used by worker modes during an `01_AI-RUN` phase.

4.  **💬 Structured `:signals` – The Swarm's Interpreted State Language:**
    `:signals` are JSON objects in [`.pheromone`](.pheromone:1), generated *exclusively* by the `✍️ @orchestrator-pheromone-scribe`'s interpretation of natural language summaries from agents executing tasks defined in [`01_AI-RUN/`](01_AI-RUN/) scripts. They influence swarm behavior and include fields like `id`, `signalType`, `target`, `category`, `strength`, `message`, `data`, and timestamps. Signal dynamics (evaporation, amplification) are governed by [`.swarmConfig`](.swarmConfig:1).

5.  **🗣️ Natural Language Summary Interpretation – The Scribe's Keystone Role:**
    Worker Agents report detailed natural language `Summary` reports of AI-verifiable outcomes (achieved by following `01_AI-RUN/` script instructions) to Task Orchestrators or directly to the `🧐 @uber-orchestrator`. These summaries are then passed to the `✍️ @orchestrator-pheromone-scribe`. The Scribe, using `interpretationLogic` from [`.swarmConfig`](.swarmConfig:1), translates this rich narrative into structured `:signals` and updates the `documentationRegistry` in [`.pheromone`](.pheromone:1) with paths to generated artifacts.

6.  **📖 Human-Centric Documentation Trail & Directory Usage within the [`01_AI-RUN/`](01_AI-RUN/) Execution Context:**
    As Pheromind agents execute the workflow defined in [`01_AI-RUN/`](01_AI-RUN/) scripts, they produce human-readable artifacts (plans, specs, code, reports). The Scribe populates a `documentationRegistry` in [`.pheromone`](.pheromone:1), tracking these documents. These documents are typically organized into specific project directories, utilized and populated as follows during the execution of the `01_AI-RUN/` workflow:
    *   **Project Root & General Docs:** Files like `README.md`, and potentially a `Master_Project_Plan.md` generated as part of an `01_AI-RUN/` phase (e.g., via [`01_AI-RUN/09_Task_Manager.md`](01_AI-RUN/09_Task_Manager.md:1)). The initial user directive itself is an `01_AI-RUN/` script.
    *   **[`01_AI-RUN/`](01_AI-RUN/):** This directory is paramount as it contains the scripts that **define the project's workflow, sequence of phases, and high-level logic**. Files like [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1) act as the main operational script for the `🧐 @uber-orchestrator`, dictating the progression through various project stages by referencing other `01_AI-RUN/*.md` scripts. These other scripts (e.g., [`01_AI-RUN/01_Getting_Started.md`](01_AI-RUN/01_Getting_Started.md:1), [`01_AI-RUN/03_Idea.md`](01_AI-RUN/03_Idea.md:1)) provide detailed instructions, templates, or logic for specific phases, which Pheromind agents (defined in [`.roomodes`](.roomodes:1)) execute. The `Original_User_Directive_Payload_Path_Field` in the `🎩 @head-orchestrator`'s initial parameters directly points to an entry-point script in this directory, making it the primary driver for the Pheromind execution engine.
    *   **[`02_AI-DOCS/`](02_AI-DOCS/):** This is a primary location for technical documentation generated by Worker Agents (e.g., `🏛️ @architect-highlevel-module`, `📚 @docs-writer-feature`, `orchestrator-technical-documentation`) as they execute tasks defined in [`01_AI-RUN/`](01_AI-RUN/) scripts (like [`01_AI-RUN/07_Specs_Docs.md`](01_AI-RUN/07_Specs_Docs.md:1)). It houses architecture documents, coding/design conventions, API documentation, user manuals. The `documentationRegistry` heavily references files here.
    *   **[`03_SPECS/`](03_SPECS/):** Contains detailed specifications for features, bug fixes, etc., generated by agents like `📝 @spec-writer-feature-overview` following instructions from relevant `01_AI-RUN/` scripts (e.g., [`01_AI-RUN/06_PRD_Generation.md`](01_AI-RUN/06_PRD_Generation.md:1)). These are critical inputs for development and testing agents executing subsequent `01_AI-RUN/` phases. The `documentationRegistry` tracks these specifications.
    *   **`research_*` directories (e.g., [`research_context7/`](research_context7/), [`research_mcp_integration/`](research_mcp_integration/)):** When an `01_AI-RUN/` script (e.g., [`01_AI-RUN/04_Market_Research.md`](01_AI-RUN/04_Market_Research.md:1)) dictates a research phase, specialized research agents (e.g., `🔎 @research-planner-strategic`) store their findings, analyses, and reports within these structured directories. Key outputs are registered in the `documentationRegistry`.
    *   **`src/`:** Contains the source code generated by Pheromind agents (e.g., `👨‍💻 @coder-test-driven`) during implementation phases (e.g., executing [`01_AI-RUN/08_Start_Building.md`](01_AI-RUN/08_Start_Building.md:1)).
    *   **`tasks/`:** Contains task management files like [`tasks/tasks.json`](tasks/tasks.json:1), populated by agents like `orchestrator-sparc-specification-master-test-plan` or the `🧐 @uber-orchestrator` (when using the `taskmaster-ai` MCP) as per the [`01_AI-RUN/09_Task_Manager.md`](01_AI-RUN/09_Task_Manager.md:1) script.
    The `🧐 @uber-orchestrator` and its delegated Pheromind agents (defined in [`.roomodes`](.roomodes:1)) utilize these directories for context and to store their deliverables as specified by the `01_AI-RUN/` scripts, ensuring all outputs are part of the AI-verifiable process and human-auditable trail.

7.  **Key File Ecosystem:**
    *   **[`.pheromone`](.pheromone:1):** The central JSON file holding `:signals` (tracking the last completed `01_AI-RUN` phase and other state) and `documentationRegistry`. Exclusively managed by the `✍️ @orchestrator-pheromone-scribe` based on the outcomes of `01_AI-RUN/` script executions.
    *   **[`.swarmConfig`](.swarmConfig:1):** A user-created JSON file defining the Scribe's `interpretationLogic` and rules for signal dynamics. Read by the Scribe, never modified by it.
    *   **[`.roomodes`](.roomodes:1):** JSON definitions for all Pheromind agents, including their roles, `customInstructions` (which detail how they execute specific `01_AI-RUN/` phases or tasks), and capabilities. This file is critical for how the `🧐 @uber-orchestrator` delegates tasks and how worker agents execute the `01_AI-RUN/` workflows.

## General Pheromind Workflow Diagram

The diagram below illustrates the interaction between Pheromind agents and the key files, emphasizing that the Pheromind system **executes the workflow defined by the [`01_AI-RUN/`](01_AI-RUN/) scripts**. The `Original_User_Directive_Payload_Path_Field` provided to the `🎩 @head-orchestrator` (and subsequently to the `🧐 @uber-orchestrator`) points to an entry-point script within the [`01_AI-RUN/`](01_AI-RUN/) directory (e.g., [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1)). This script serves as the primary blueprint for the `🧐 @uber-orchestrator`, defining the sequence of project phases and referencing other `01_AI-RUN/*.md` files for detailed phase-specific instructions which are then executed by the appropriate Pheromind agents as per [`.roomodes`](.roomodes:1).

```mermaid
graph TD
    subgraph User Interaction
        UI[User: Initial Directive (Path to 01_AI-RUN Script like 02_AutoPilot.md) & Parameters]
    end

    subgraph Pheromind Core Cycle - Execution of 01_AI-RUN/ Workflow
        HO["🎩 @head-orchestrator (Plan Custodian Initiator)"]
        UO["🧐 @uber-orchestrator (Pheromone-Guided Delegator - Uses 01_AI-RUN/ entry script & .roomodes for agent delegation)"]
        TSO_WA["Task-Specific Orchestrators & Worker Agents (e.g., 🌟, 🛠️, ⚙️, 👨‍💻, 📝, 🧪, 🔎 - Execute specific 01_AI-RUN/ phase scripts based on .roomodes definitions)"]
        PS["✍️ @orchestrator-pheromone-scribe (Interpreter & State Manager for 01_AI-RUN/ progress)"]
    end

    subgraph Key Files & Directories - Supporting 01_AI-RUN/ Execution
        PHEROMONE[".pheromone (Signals & Docs Registry - Tracks 01_AI-RUN/ phase state)"]
        SWARMCONFIG[".swarmConfig (Scribe's InterpretationLogic for 01_AI-RUN/ summaries)"]
        ROOMODES[".roomodes (Agent Definitions, including 01_AI-RUN execution logic)"]
        AIRUN_SCRIPTS["01_AI-RUN/ (Directory containing *.md workflow scripts - THE BLUEPRINT)"]
        AIRUN_ENTRY["01_AI-RUN/02_AutoPilot.md (Example Entry Point Script for UO)"]
        AIRUN_PHASE_SCRIPT["01_AI-RUN/03_Idea.md (Example Phase-Specific Script for delegated Agent)"]
        OUTPUT_DOCS["02_AI-DOCS/, 03_SPECS/, research_*/, src/, tasks/ (Outputs of 01_AI-RUN/ phases)"]
    end

    UI -- Provides Path to Entry-Point 01_AI-RUN Script & Params --> HO
    HO -- Passes Path & Params --> UO

    PS -.->|Bootstraps (if new)| PHEROMONE
    PS -- Reads/Writes --> PHEROMONE
    PS -- Reads --> SWARMCONFIG
    
    UO -- Reads --> PHEROMONE
    UO -- Uses --> AIRUN_ENTRY
    UO -- Reads --> ROOMODES
    UO -- Delegates Phase (based on AIRUN_ENTRY, .pheromone state & .roomodes) --> TSO_WA
    
    TSO_WA -- Reads --> PHEROMONE
    TSO_WA -- Uses --> AIRUN_PHASE_SCRIPT
    TSO_WA -- Reads --> ROOMODES
    TSO_WA -- Execute Task (defined in AIRUN_PHASE_SCRIPT, guided by .roomodes) --> Outcome["Produces AI-Verifiable Outcome (Code, Docs, Specs, Research Reports as per 01_AI-RUN/ script)"]
    Outcome -- Stored in --> OUTPUT_DOCS
    TSO_WA -- NL Summary (Verifiable Outcome Report for 01_AI-RUN/ task) --> UO
    
    UO -- Aggregated NL Summary (01_AI-RUN/ Phase Outcome Report, or directly from WA) --> PS
    
    PS -- Interprets NL Summary (using SWARMCONFIG) --> PHEROMONE_Update["Updates :signals & documentationRegistry in .pheromone reflecting 01_AI-RUN/ progress"]
    PHEROMONE_Update --> PHEROMONE
    PS -- Activates --> HO

    %% Agent Definitions are central
    HO --- ROOMODES
    UO --- ROOMODES
    TSO_WA --- ROOMODES
    PS --- ROOMODES

    %% Workflow Definition is central
    AIRUN_SCRIPTS -- Defines Workflow --> UO
    AIRUN_SCRIPTS -- Defines Workflow --> TSO_WA
    
    %% Documentation Flow
    OUTPUT_DOCS <-.-> PHEROMONE_Update_Docs["documentationRegistry in .pheromone tracks outputs of 01_AI-RUN/ phases"]


    classDef agent fill:#f9f,stroke:#333,stroke-width:2px;
    classDef file fill:#ccf,stroke:#333,stroke-width:2px;
    classDef dir fill:#cfc,stroke:#333,stroke-width:2px;
    class HO,UO,TSO_WA,PS agent;
    class PHEROMONE,SWARMCONFIG,ROOMODES,AIRUN_ENTRY,AIRUN_PHASE_SCRIPT file;
    class AIRUN_SCRIPTS,OUTPUT_DOCS dir;
```

## Detailed Pheromind Workflow: The "Boomerang Task" Lifecycle as Execution of [`01_AI-RUN/`](01_AI-RUN/) Scripts

Pheromind operates on a cyclical "Boomerang Task" pattern, acting as the **execution engine** for the workflow defined in the [`01_AI-RUN/`](01_AI-RUN/) scripts. Tasks, derived from these scripts and agent definitions in [`.roomodes`](.roomodes:1), are delegated downwards by the `🧐 @uber-orchestrator` with AI-verifiable criteria. These are executed by Pheromind worker agents, and results are reported upwards via natural language summaries. The `✍️ @orchestrator-pheromone-scribe` interprets these summaries to update the shared state in [`.pheromone`](.pheromone:1), which, along with the `01_AI-RUN/` scripts and [`.roomodes`](.roomodes:1), guides the next cycle.

**State Management Note:** Throughout this lifecycle, [`.pheromone`](.pheromone:1) is the primary state mechanism, recording signals of `01_AI-RUN` phase completions and paths to generated artifacts. If a legacy `project_session_state.json` file is generated as an output of an `01_AI-RUN/` script, it is treated as any other document: its path is recorded in the `documentationRegistry` by the Scribe, but it does not drive the core operational state of the Pheromind swarm.

### Phase 0: Foundational Setup & Initiation (Executing Initial [`01_AI-RUN/`](01_AI-RUN/) Scripts)

This phase prepares the environment and launches the Pheromind swarm to execute the initial stages of the project as defined in the entry-point `01_AI-RUN/` script and guided by [`.roomodes`](.roomodes:1).

*   **User Actions (Pre-computation):**
    1.  **Environment Configuration:** Ensure a compatible Roo Code environment and configured LLM (e.g., Claude 3.x) with API keys.
    2.  **Define Agent Behaviors ([`.roomodes`](.roomodes:1)):** Create/review the JSON file in the project root defining all agents, including their `customInstructions` for executing `01_AI-RUN` phases.
    3.  **Establish Scribe's Rulebook ([`.swarmConfig`](.swarmConfig:1)):** User creates this JSON file containing `interpretationLogic`, signal dynamics, and definitions.
    4.  **Prepare Initial Directive (Entry-Point [`01_AI-RUN/`](01_AI-RUN/) Script):** The primary initial directive is an entry-point script within the [`01_AI-RUN/`](01_AI-RUN/) directory, typically [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1). This script outlines the overall project flow and references other `01_AI-RUN/*.md` files for specific phase instructions.

*   **Swarm Initiation (User Action):**
    1.  **Activate `🎩 @head-orchestrator`:** The user initiates the workflow by activating this agent with parameters including:
        *   `Original_User_Directive_Payload_Path_Field`: Path to the entry-point `01_AI-RUN/` script (e.g., [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1)).
        *   Other necessary paths like `Original_Project_Root_Path_Field` and `Pheromone_File_Path`.

*   **First "Boomerang" - Startup Logic & Execution of Initial `01_AI-RUN/` Phase:**
    1.  **`🎩 @head-orchestrator` -> `🧐 @uber-orchestrator`:** Passes the directive (path to the `01_AI-RUN/` script) and parameters.
    2.  **`✍️ @orchestrator-pheromone-scribe` (Implicit First Action):** Bootstraps [`.pheromone`](.pheromone:1) if missing and loads [`.swarmConfig`](.swarmConfig:1).
    3.  **`🧐 @uber-orchestrator` Initial Assessment & Execution (as per "01_AI-RUN Workflow Orchestration" in [`.roomodes`](.roomodes:1)):**
        *   Reads [`.pheromone`](.pheromone:1) to check for the last completed `01_AI-RUN` phase.
        *   Accesses the entry-point `01_AI-RUN/` script (e.g., [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1)).
        *   Its primary goal is to **execute the sequence defined in this script**, determining the next `01_AI-RUN` phase.
    4.  **Delegation for "Getting Started" Phase (Executing [`01_AI-RUN/01_Getting_Started.md`](01_AI-RUN/01_Getting_Started.md:1)):**
        *   The `🧐 @uber-orchestrator`, following its logic in [`.roomodes`](.roomodes:1) and the sequence in [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1), identifies the "Getting Started" phase.
        *   It tasks the `code-comprehension-assistant-v2` agent with executing the [`01_AI-RUN/01_Getting_Started.md`](01_AI-RUN/01_Getting_Started.md:1) sub-prompt, as per `uber-orchestrator`'s and `code-comprehension-assistant-v2`'s `customInstructions` in [`.roomodes`](.roomodes:1).
    5.  **Execution by `code-comprehension-assistant-v2` (Following [`01_AI-RUN/01_Getting_Started.md`](01_AI-RUN/01_Getting_Started.md:1)):**
        *   The `code-comprehension-assistant-v2` agent executes the steps outlined in [`01_AI-RUN/01_Getting_Started.md`](01_AI-RUN/01_Getting_Started.md:1). This typically includes:
            *   "AI Agent Initial Onboarding" steps.
            *   "Codebase Xray" analysis.
        *   **Output Example:** As per [`01_AI-RUN/01_Getting_Started.md`](01_AI-RUN/01_Getting_Started.md:1), this could be the generation of `codebase_xray_analysis.json` stored in [`03_SPECS/`](03_SPECS/).
        *   A `Master_Project_Plan.md` might also be initiated or referenced if dictated by [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1) or [`01_AI-RUN/01_Getting_Started.md`](01_AI-RUN/01_Getting_Started.md:1), to be fully populated later (e.g., by `orchestrator-sparc-specification-master-test-plan` executing [`01_AI-RUN/09_Task_Manager.md`](01_AI-RUN/09_Task_Manager.md:1)).
    6.  **Reporting to Scribe (`code-comprehension-assistant-v2` -> `🧐 @uber-orchestrator` -> `✍️ @orchestrator-pheromone-scribe`):**
        *   `code-comprehension-assistant-v2` compiles a natural language summary detailing completion of tasks from [`01_AI-RUN/01_Getting_Started.md`](01_AI-RUN/01_Getting_Started.md:1), lists outputs, and confirms AI-verifiable outcomes. This summary is passed to the `🧐 @uber-orchestrator`.
        *   The `🧐 @uber-orchestrator` forwards this summary to the `✍️ @orchestrator-pheromone-scribe`.
    7.  **Scribe Interpretation & State Update (`✍️ @orchestrator-pheromone-scribe`):**
        *   The Scribe interprets the summary.
        *   Generates initial `:signals` (e.g., `getting_started_phase_complete`, `codebase_analysis_available`).
        *   Populates the `documentationRegistry` in [`.pheromone`](.pheromone:1) with entries for the `01_AI-RUN/` scripts used and paths to outputs.
        *   Persists changes to [`.pheromone`](.pheromone:1).
    8.  **Cycle Completion & Re-activation:** The Scribe activates the `🎩 @head-orchestrator`.

*   **Why:** This phase uses the initial `01_AI-RUN/` scripts and agent definitions in [`.roomodes`](.roomodes:1) to set up the project, perform initial analyses, and establish a baseline state in [`.pheromone`](.pheromone:1]. The Pheromind system acts as the direct executor of these scripted instructions.

### Phase 1: Iterative Development & Execution (Pheromind Executing Subsequent [`01_AI-RUN/`](01_AI-RUN/) Defined Phases)

This is a cyclical phase where Pheromind executes the core project work, phase by phase, as dictated by the main `01_AI-RUN/` script (e.g., [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1)), detailed in phase-specific `01_AI-RUN/*.md` files, and executed by agents defined in [`.roomodes`](.roomodes:1).

1.  **Strategic Delegation by `🧐 @uber-orchestrator` (Following [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1) and [`.roomodes`](.roomodes:1)):**
    *   The `🧐 @uber-orchestrator` consults the updated [`.pheromone`](.pheromone:1] (for the last completed `01_AI-RUN` phase signal) and the sequence in [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1) to identify the next phase (e.g., "Idea Generation").
    *   Based on its "01_AI-RUN Workflow Orchestration" logic in [`.roomodes`](.roomodes:1), it delegates this phase to the appropriate Pheromind agent, providing the path to the relevant `01_AI-RUN/*.md` script as the primary set of instructions.

2.  **Phase Execution by Delegated Pheromind Agents (Following Specific `01_AI-RUN/*.md` Scripts and their `customInstructions` in [`.roomodes`](.roomodes:1)):**
    *   The assigned Pheromind agent uses the provided `01_AI-RUN/*.md` script and its own `customInstructions` from [`.roomodes`](.roomodes:1) for the current phase.
    *   **Example: Idea Generation (Executing [`01_AI-RUN/03_Idea.md`](01_AI-RUN/03_Idea.md:1))**
        *   The `🧐 @uber-orchestrator` tasks `research-planner-strategic` with executing the [`01_AI-RUN/03_Idea.md`](01_AI-RUN/03_Idea.md:1) script.
        *   `research-planner-strategic` meticulously follows the steps in [`01_AI-RUN/03_Idea.md`](01_AI-RUN/03_Idea.md:1) and its "01_AI-RUN 'Idea' Phase Execution" `customInstructions`.
        *   This involves performing actions like generating content for `idea_document.md`.
        *   The output is saved to the path specified in the script or by convention (e.g., `research_context7/initial_queries/scope_definition.md`).
        *   The AI-verifiable outcome is confirmed.
        *   If [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1) specifies user validation for this phase, `research-planner-strategic` uses `ask_followup_question`. The response is routed back through `🧐 @uber-orchestrator` before the phase is marked complete.
    *   **Subsequent Phases (Executed by agents as per [`.roomodes`](.roomodes:1) and `01_AI-RUN/` scripts):**
        *   **Market Research:** `🧐 @uber-orchestrator` tasks `research-planner-strategic` with [`01_AI-RUN/04_Market_Research.md`](01_AI-RUN/04_Market_Research.md:1). Agent stores findings in `research_*` directories.
        *   **Core Concept Definition:** `🧐 @uber-orchestrator` tasks `research-planner-strategic` with [`01_AI-RUN/05_Core_Concept.md`](01_AI-RUN/05_Core_Concept.md:1). Agent produces documents like `core_concept_definition.md`.
        *   **PRD Generation:** `🧐 @uber-orchestrator` tasks `spec-writer-feature-overview` with [`01_AI-RUN/06_PRD_Generation.md`](01_AI-RUN/06_PRD_Generation.md:1). Agent uses templates to create `project_prd.md` in [`03_SPECS/`](03_SPECS/).
        *   **Specs & Docs:** `🧐 @uber-orchestrator` tasks `orchestrator-technical-documentation` with [`01_AI-RUN/07_Specs_Docs.md`](01_AI-RUN/07_Specs_Docs.md:1). Agent populates [`02_AI-DOCS/`](02_AI-DOCS/) and [`03_SPECS/`](03_SPECS/).
        *   **Task Management Setup:** `🧐 @uber-orchestrator` tasks `orchestrator-sparc-specification-master-test-plan` (or itself if the script involves direct MCP tool use like `taskmaster-ai`) with [`01_AI-RUN/09_Task_Manager.md`](01_AI-RUN/09_Task_Manager.md:1). Agent populates [`tasks/tasks.json`](tasks/tasks.json:1).
        *   **Implementation (Start Building):** `🧐 @uber-orchestrator` tasks `coder-test-driven` with [`01_AI-RUN/08_Start_Building.md`](01_AI-RUN/08_Start_Building.md:1). Agent writes code into `src/` based on tasks and specs, following its "01_AI-RUN 'Implementation' Phase Execution" `customInstructions`.

3.  **Worker Execution & AI-Verified Output (as per `01_AI-RUN/*.md` and [`.roomodes`](.roomodes:1)):**
    *   Worker Agents execute their assigned tasks, strictly following the logic within the specific `01_AI-RUN/*.md` for their current phase and their `customInstructions` in [`.roomodes`](.roomodes:1).
    *   They produce deliverables and a detailed natural language `Summary` confirming the AI-verifiable outcome.

4.  **Summary Handoff to Scribe & State Evolution:**
    *   The agent responsible for the phase sends its summary to the `🧐 @uber-orchestrator`, which then passes it to the `✍️ @orchestrator-pheromone-scribe`.
    *   The Scribe interprets the summary.
    *   Updates `:signals` (e.g., `market_research_complete`, `prd_generated_successfully`) and the `documentationRegistry` in [`.pheromone`](.pheromone:1).
    *   Activates the `🎩 @head-orchestrator`.

5.  **Cycle Continuation & Adaptation (Guided by [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1) and [`.pheromone`](.pheromone:1)):**
    *   The `🧐 @uber-orchestrator` reads the newly updated [`.pheromone`](.pheromone:1] and consults [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1) to determine the next phase and its corresponding `01_AI-RUN/*.md` script, delegating to the agent specified in [`.roomodes`](.roomodes:1).

*   **Why:** This iterative cycle, driven by the `01_AI-RUN/` scripts and orchestrated by agents defined in [`.roomodes`](.roomodes:1), allows Pheromind to systematically build the project. The scripts provide the "program," and [`.roomodes`](.roomodes:1) defines "who" executes which part.

### Phase 2: Integration, System Testing, and Refinement (Executing [`01_AI-RUN/10_Testing.md`](01_AI-RUN/10_Testing.md:1))

*   Following the sequence in [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1), once implementation phases signal completion, the `🧐 @uber-orchestrator` delegates testing.
*   It tasks `tester-tdd-master` with executing the instructions within [`01_AI-RUN/10_Testing.md`](01_AI-RUN/10_Testing.md:1), guided by its "01_AI-RUN 'Testing' Phase Execution" `customInstructions` in [`.roomodes`](.roomodes:1).
*   This involves running integration tests, system-wide tests, and end-to-end test plans.
*   Successful execution of these tests, as defined in [`01_AI-RUN/10_Testing.md`](01_AI-RUN/10_Testing.md:1), are AI-verifiable outcomes.
*   Refinement cycles are managed by orchestrators like `🔄 @orchestrator-refinement-and-maintenance`.

*   **Why:** Ensures the system built by executing the `01_AI-RUN/` implementation scripts meets quality standards, with Pheromind managing the execution of the testing workflow itself as defined by scripts and agent roles.

### Phase 3: Deployment (Executing [`01_AI-RUN/11_Deployment.md`](01_AI-RUN/11_Deployment.md:1))

*   Once testing is satisfactory, the `🧐 @uber-orchestrator`, following [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1), delegates deployment.
*   It tasks `devops-pipeline-manager` with executing the steps detailed in [`01_AI-RUN/11_Deployment.md`](01_AI-RUN/11_Deployment.md:1), guided by its "01_AI-RUN 'Deployment' Phase Execution" `customInstructions` in [`.roomodes`](.roomodes:1).
*   This may involve using deployment guides and interacting with CI/CD tools.
*   AI-verifiable outcomes are defined in [`01_AI-RUN/11_Deployment.md`](01_AI-RUN/11_Deployment.md:1).

*   **Why:** Pheromind executes the deployment process as scripted in [`01_AI-RUN/11_Deployment.md`](01_AI-RUN/11_Deployment.md:1) and defined in [`.roomodes`](.roomodes:1), ensuring a consistent and verifiable release.

### Phase 4: Post-Deployment & Iteration (Re-engaging with [`01_AI-RUN/`](01_AI-RUN/) Workflows)

*   Pheromind's lifecycle, as an execution engine for `01_AI-RUN/` scripts, is continuous.
*   New feature requests or bug reports are fed as new directives, typically by providing a path to an appropriate `01_AI-RUN/` script.
*   The existing [`.pheromone`](.pheromone:1], [`.roomodes`](.roomodes:1), and the library of `01_AI-RUN/` scripts provide the context and procedures for ongoing work.

*   **Why:** Enables continuous product improvement and maintenance, with Pheromind consistently executing defined `01_AI-RUN/` workflows, leveraging past state, established procedures, and defined agent roles.

This detailed workflow, centered around the `✍️ @orchestrator-pheromone-scribe`, the `🧐 @uber-orchestrator`'s execution of [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1), and the delegation to specialized agents defined in [`.roomodes`](.roomodes:1) to execute specific `01_AI-RUN/*.md` scripts, allows Pheromind to autonomously **execute the project lifecycle**. It does so by effectively utilizing these scripts as instructions, managing state in [`.pheromone`](.pheromone:1), and populating a structured system of project directories through its specialized agents.