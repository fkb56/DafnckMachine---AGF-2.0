# Pheromind: The AI Swarm Execution Engine for 01_AI-RUN Workflows

This document outlines the operational workflow of the Pheromind system, the AI swarm that serves as the execution engine and state management layer for the project lifecycle defined by the scripts within the [`01_AI-RUN/`](01_AI-RUN/) directory. Pheromind orchestrates software development from idea to deployment, driven by AI agents and structured [`01_AI-RUN/`](01_AI-RUN/) phase definitions.

## Workflow Diagram

```mermaid
graph TD
    subgraph Pheromind System
        HO[🎩 @head-orchestrator] -- Initiates with 01_AI-RUN Script --> UO{🧐 @uber-orchestrator}
        UO -- Reads & Executes --> AIRUN[01_AI-RUN/*.md Scripts]
        AIRUN -- Defines Phases & Logic --> UO
        UO -- Delegates Phase Task --> SA[Specialized Agent (e.g., @coder, @tester)]
        SA -- Performs Task based on AIRUN Script --> SANL[NL Summary of Task Output & Artifacts]
        SANL -- Sends to --> Scribe[✍️ @orchestrator-pheromone-scribe]
        Scribe -- Updates State & Doc Registry --> PheromoneDB[(.pheromone)]
        PheromoneDB -- Provides Current State & Context --> UO
        PheromoneDB -- Provides Current State & Context --> SA
        SA -- Generates --> Docs[Project Documents e.g., in 02_AI-DOCS/, 03_SPECS/]
        Scribe -- Records Path in documentationRegistry --> Docs
        SA -- User Validation Point in AIRUN Script? --> UV{User Validation Needed}
        UV -- Yes --> Ask[Agent uses ask_followup_question]
        Ask --> UserInput[User Input/Approval via UI]
        UserInput -- Informs --> SA
        UV -- No --> SANL
    end

    subgraph Configuration Files
        Roomodes[(.roomodes defines Agent Roles)]
        SwarmConfig[(.swarmConfig defines Scribe Logic)]
    end

    HO -- Guided by --> Roomodes
    HO -- Guided by --> SwarmConfig
    UO -- Guided by --> Roomodes
    UO -- Guided by --> SwarmConfig
    SA -- Role Defined by --> Roomodes
    Scribe -- InterpretationLogic from --> SwarmConfig

    style PheromoneDB fill:#f9f,stroke:#333,stroke-width:2px
    style AIRUN fill:#ccf,stroke:#333,stroke-width:2px
    style Docs fill:#cfc,stroke:#333,stroke-width:2px
```

## Key Operational Principles

The Pheromind system's execution of the [`01_AI-RUN/`](01_AI-RUN/) workflow is governed by the following core principles:

### Pheromind as the Execution Engine for [`01_AI-RUN/`](01_AI-RUN/) Workflows
*   The Pheromind system, comprising specialized AI agents (defined in [`.roomodes`](.roomodes:1)), the `✍️ @orchestrator-pheromone-scribe`, the [`.pheromone`](.pheromone:1) state file, and the [`.swarmConfig`](.swarmConfig:1), acts as the primary execution engine and state management layer for the entire project lifecycle.
*   The sequence of project phases, high-level logic, specific instructions, and user validation points for each phase are explicitly defined within the markdown scripts located in the [`01_AI-RUN/`](01_AI-RUN/) directory (e.g., [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1)). These scripts constitute the authoritative definition of the workflow.
*   Pheromind agents, primarily orchestrated by the `🧐 @uber-orchestrator`, meticulously read and execute these [`01_AI-RUN/`](01_AI-RUN/) scripts sequentially, treating their instructions as direct commands for progressing the project.

### Pheromone-Based Swarm Intelligence (Stigmergy)
*   Pheromind leverages stigmergy, a form of indirect coordination where agents interact by modifying a shared environment—the [`.pheromone`](.pheromone:1) JSON file.
*   The [`.pheromone`](.pheromone:1) file serves as the swarm's collective memory and central state tracker. It records the completion status of each phase detailed in the [`01_AI-RUN/`](01_AI-RUN/) scripts, paths to all generated documents (via the `documentationRegistry`), critical decisions, user inputs, and overall project progress.
*   This mechanism enables robust, asynchronous, and contextually-aware task distribution and execution across the diverse Pheromind agents.

### AI-Verifiable Project Execution
*   The workflow is designed around AI-verifiable outcomes. Criteria for successful phase completion and task execution are often embedded within the instructional text of the [`01_AI-RUN/`](01_AI-RUN/) scripts or are derived into a Master Project Plan that guides agent actions.
*   Agents are programmed to assess their outputs against these criteria, ensuring that each step aligns with the project goals as defined by the [`01_AI-RUN/`](01_AI-RUN/) workflow and, ultimately, the high-level acceptance tests of the project.

### Autonomous Task Orchestration by Pheromind Agents
*   The `🎩 @head-orchestrator` initiates the entire workflow by invoking the `🧐 @uber-orchestrator` with a designated entry-point script from the [`01_AI-RUN/`](01_AI-RUN/) directory (e.g., [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1)).
*   The `🧐 @uber-orchestrator` then autonomously drives the project by sequentially processing the phases and instructions within that entry script and any subsequent [`01_AI-RUN/`](01_AI-RUN/) scripts it is directed to execute.
*   For specific tasks within each [`01_AI-RUN/`](01_AI-RUN/) phase (like documentation, coding, or testing), the `🧐 @uber-orchestrator` delegates to specialized Pheromind agents (e.g., `📚 @docs-writer-feature`, `👨‍💻 @coder-test-driven`) whose roles and capabilities are defined in [`.roomodes`](.roomodes:1).
*   Explicit user validation points embedded within the [`01_AI-RUN/`](01_AI-RUN/) scripts are managed by the relevant agent using the `ask_followup_question` tool, ensuring human-in-the-loop oversight at critical junctures.

### The `✍️ @orchestrator-pheromone-scribe` and State Integrity
*   The `✍️ @orchestrator-pheromone-scribe` is a vital agent singularly focused on maintaining the accuracy and integrity of the [`.pheromone`](.pheromone:1) state file.
*   Upon completion of tasks related to an [`01_AI-RUN/`](01_AI-RUN/) phase, specialized agents submit natural language (NL) summaries of their work and list any generated artifacts.
*   The Scribe, utilizing `interpretationLogic` defined in [`.swarmConfig`](.swarmConfig:1), parses these NL summaries to precisely update the [`.pheromone`](.pheromone:1) file with new state information, document paths (populating the `documentationRegistry`), and markers for phase completion.

### Configuration-Driven Adaptability ([`.swarmConfig`](.swarmConfig:1) & [`.roomodes`](.roomodes:1))
*   The specific behaviors, roles, expertise, and operational parameters (like LLM choice) of Pheromind agents are defined and configured through the [`.roomodes`](.roomodes:1) JSON file. This allows for a flexible and adaptable swarm.
*   The [`.swarmConfig`](.swarmConfig:1) file, especially its `interpretationLogic` section, provides the ruleset for how the `✍️ @orchestrator-pheromone-scribe` translates agent NL summaries into structured updates for the [`.pheromone`](.pheromone:1) state.
*   Together, these configuration files enable Pheromind's execution of the [`01_AI-RUN/`](01_AI-RUN/) workflow to be highly tailored and consistently managed.

### Human-Centric Documentation Trail
*   As Pheromind agents execute the phases defined in the [`01_AI-RUN/`](01_AI-RUN/) scripts, they produce a comprehensive suite of project documents (e.g., `idea_document.md`, `project_prd.md`, technical specifications, architectural diagrams, source code, test plans, and reports).
*   These artifacts are systematically organized and stored in designated project directories like [`02_AI-DOCS/`](02_AI-DOCS/), [`03_SPECS/`](03_SPECS/), and the primary source code directories.
*   The `✍️ @orchestrator-pheromone-scribe` diligently records the paths to these generated documents in the `documentationRegistry` section of the [`.pheromone`](.pheromone:1) file. This creates a persistent, traceable, and human-accessible audit trail of the project's development, directly mapping outputs to the executed [`01_AI-RUN/`](01_AI-RUN/) workflow phases.

### Cyclical "Boomerang Task" Lifecycle for [`01_AI-RUN/`](01_AI-RUN/) Phases
*   The execution of each distinct phase or sub-task outlined in an [`01_AI-RUN/`](01_AI-RUN/) script adheres to a cyclical "boomerang task" pattern:
    1.  The `🧐 @uber-orchestrator` identifies the current phase/task from the active [`01_AI-RUN/`](01_AI-RUN/) script, using [`.pheromone`](.pheromone:1) for context.
    2.  It delegates this specific phase/task to an appropriate specialized Pheromind agent, providing all necessary context and instructions from the script and [`.pheromone`](.pheromone:1).
    3.  The specialized agent performs the defined work, generating outputs such as documents, code, or analysis.
    4.  The agent then formulates a natural language summary of its actions, outcomes, and paths to any generated artifacts, sending this back (typically to the Scribe, which informs the `🧐 @uber-orchestrator` via the updated [`.pheromone`](.pheromone:1) state).
    5.  The `🧐 @uber-orchestrator`, now aware of the completed step via the updated [`.pheromone`](.pheromone:1), consults the [`01_AI-RUN/`](01_AI-RUN/) script to determine and initiate the next phase/task.
*   This iterative loop ensures that every instruction within the [`01_AI-RUN/`](01_AI-RUN/) workflow is explicitly addressed, executed by the most suitable agent, and its completion and outputs are meticulously recorded in the [`.pheromone`](.pheromone:1) state.

This document provides a high-level overview of Pheromind's operational execution of the [`01_AI-RUN/`](01_AI-RUN/) defined workflow. For more in-depth technical details, architectural specifics, and agent interactions, please refer to [`logic.md`](logic.md:1) (Pheromind Technical Manual) and [`ModeREADME.md`](ModeREADME.md:1) (Pheromind System Overview).