# 🐜 Pheromind: Autonomous AI Swarm Orchestration Framework
## 🌌 Welcome to Pheromind: The Execution Engine for AI-Driven Project Workflows

**Pheromind** is a cutting-edge AI agent orchestration framework designed to serve as the **execution engine and state management layer** for complex, multi-phase project workflows, specifically those defined by the sequence of scripts within the [`01_AI-RUN/`](01_AI-RUN/) directory (e.g., [`01_AI-RUN/01_Getting_Started.md`](01_AI-RUN/01_Getting_Started.md:1), [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1), [`01_AI-RUN/03_Idea.md`](01_AI-RUN/03_Idea.md:1)). It is particularly geared towards intricate software development lifecycles adhering to an **AI-Verifiable Methodology**, ensuring project progress is tracked through concrete, measurable, and AI-confirmable outcomes as dictated by the guiding [`01_AI-RUN/`](01_AI-RUN/) scripts.

The [`01_AI-RUN/`](01_AI-RUN/) scripts define the **"what"** (the project phases, their objectives, and deliverables) and the **"sequence"** of the project. Pheromind provides the **"how"**: its diverse collective of specialized AI agents, as defined in the [`.roomodes`](.roomodes:1) file and operating under a **pheromone-based swarm intelligence model**, interprets these [`01_AI-RUN/`](01_AI-RUN/) scripts, executes the defined phases, and manages the project's state. Agents collaborate and adapt by interacting indirectly through a shared state medium, primarily the [`.pheromone`](.pheromone:1) file.

A cornerstone of Pheromind's innovation is its `✍️ @orchestrator-pheromone-scribe`. This central agent interprets rich, natural language summaries from high-level Task Orchestrators—narratives detailing project progress and AI-verifiable results achieved during the execution of [`01_AI-RUN/`](01_AI-RUN/) phase scripts—and translates them into structured, actionable "digital pheromones" or **`:signals`** and human-centric **documentation registry** updates. These are stored in the [`.pheromone`](.pheromone:1) file, guiding the swarm's behavior, enabling dynamic task allocation, robust state management, and emergent problem-solving, all while maintaining a clear, human-auditable trail of the executed [`01_AI-RUN/`](01_AI-RUN/) workflow.

Pheromind doesn't replace the [`01_AI-RUN/`](01_AI-RUN/) workflow; it *brings it to life*, creating an adaptive, intelligent system that can navigate the complexities of modern project execution with a focus on verifiable deliverables and a level of autonomy previously unattainable, all while meticulously following the roadmap laid out in the [`01_AI-RUN/`](01_AI-RUN/) scripts.

---

## ✨ Core Concepts: Understanding the Pheromind Swarm

To grasp the power of Pheromind, familiarize yourself with these foundational principles:

*   **🧠 Pheromone-Based Swarm Intelligence (Stigmergy):**
    Inspired by social insects, Pheromind agents interact indirectly through a shared environment – the [`.pheromone`](.pheromone:1) file. This file contains structured JSON `:signals` representing the interpreted state of the project (derived from the execution of the [`01_AI-RUN/`](01_AI-RUN/) workflow) and a `documentationRegistry` tracking human-readable project artifacts generated as per that workflow. Agents "sense" these signals, and Task Orchestrators provide natural language summaries of phase execution (based on [`01_AI-RUN/`](01_AI-RUN/) scripts) that the `✍️ @orchestrator-pheromone-scribe` uses to "deposit" new trails. This "pheromone landscape" guides agent actions, fostering decentralized yet coordinated work in executing the defined project plan.

*   **🎯 AI-Verifiable Project Execution (Driven by [`01_AI-RUN/`](01_AI-RUN/)):**
    Pheromind *executes* workflows, such as those defined in the [`01_AI-RUN/`](01_AI-RUN/) directory, which champion a methodology where project progression is defined by tasks with **AI-Verifiable End Results**. For instance, an initial [`01_AI-RUN/`](01_AI-RUN/) script might direct the `🧐 @uber-orchestrator` to task an agent like `🌟 @orchestrator-sparc-specification-master-test-plan` to create a **Master Project Plan**. This plan, itself an output of an [`01_AI-RUN/`](01_AI-RUN/) phase, details further phases and micro-tasks, each with specific, programmatically checkable completion criteria (e.g., file existence with correct schema as specified in an [`01_AI-RUN/`](01_AI-RUN/) script, script execution without error, all tests in a suite passing). Task Orchestrators ensure their delegated worker tasks adhere to these verifiable outcomes, making progress unambiguous and AI-auditable as the swarm executes the overall [`01_AI-RUN/`](01_AI-RUN/) sequence.

*   **⚙️ Autonomous Task Orchestration (Executing the [`01_AI-RUN/`](01_AI-RUN/) Workflow):**
    Once initiated with a high-level objective, typically an entry-point script from the [`01_AI-RUN/`](01_AI-RUN/) directory (e.g., [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1)), Pheromind autonomously manages the execution of this defined workflow. The `🧐 @uber-orchestrator` strategically delegates phases outlined in the *active* [`01_AI-RUN/`](01_AI-RUN/) script to appropriate Task-Specific Orchestrators or Worker Agents (as per its `customInstructions` in [`.roomodes`](.roomodes:1)), guided by the current [`.pheromone`](.pheromone:1) state. These agents, in turn, execute their assigned tasks, ensuring each task has an AI-verifiable end result as specified or implied by the [`01_AI-RUN/`](01_AI-RUN/) instructions for that phase. Progress, reported as rich natural language summaries detailing these verifiable outcomes, is processed by the `✍️ @orchestrator-pheromone-scribe` to update the global state, allowing the system to dynamically adjust its strategy while progressing through the [`01_AI-RUN/`](01_AI-RUN/) sequence.

*   **💬 Structured `:signals` – The Language of the Swarm's Interpreted State:**
    `:signals` are the lifeblood of Pheromind's internal state representation. Generated *exclusively* by the `✍️ @orchestrator-pheromone-scribe`'s interpretation of natural language summaries (which report on the execution of tasks defined in or derived from [`01_AI-RUN/`](01_AI-RUN/) scripts), they are machine-readable, structured JSON objects stored in the [`.pheromone`](.pheromone:1) file's `signals` array. Each `:signal` influences swarm behavior and typically includes:
    *   `id`, `signalType`, `target`, `category`, `strength`, `message`, `data` (extracted specifics), `timestamp_created` & `last_updated_timestamp`.
    These `:signals` are dynamic, subject to rules (evaporation, amplification, pruning) governed by the separate [`.swarmConfig`](.swarmConfig:1) file, which the Scribe uses.

*   **🗣️ Natural Language Summary Interpretation – The Scribe's Keystone Role:**
    This is where Pheromind translates complex progress (from executing [`01_AI-RUN/`](01_AI-RUN/) phases) into structured state:
    1.  **Worker Agents** complete granular tasks (defined by or derived from [`01_AI-RUN/`](01_AI-RUN/) scripts), producing AI-verifiable outputs (e.g., a spec file, tested code) and a detailed, **natural language `Summary` report** of their actions, outcomes, and verification status for their parent Task Orchestrator.
    2.  **Task-Specific Orchestrators** (or the `🧐 @uber-orchestrator` if directly tasking workers for an [`01_AI-RUN/`](01_AI-RUN/) phase) aggregate these worker summaries and details of their own phase-management activities (which also involve tracking AI-verifiable phase goals from the [`01_AI-RUN/`](01_AI-RUN/) workflow) into a single, comprehensive **natural language summary report**.
    3.  This narrative is dispatched to the **`✍️ @orchestrator-pheromone-scribe`**.
    4.  The **`✍️ @orchestrator-pheromone-scribe`**, using sophisticated `interpretationLogic` (defined in the external [`.swarmConfig`](.swarmConfig:1) file), *translates* this rich natural language summary into precise, **structured JSON `:signals`** and updates to the `documentationRegistry` within the [`.pheromone`](.pheromone:1) file. This unique capability allows the swarm to react to nuanced updates from the workflow execution, beyond rigid protocols, and track human-readable documentation generated as per the [`01_AI-RUN/`](01_AI-RUN/) plan.

*   **📖 Human-Centric Documentation Trail (Outputs of [`01_AI-RUN/`](01_AI-RUN/)):**
    Throughout the project, as Pheromind executes the [`01_AI-RUN/`](01_AI-RUN/) workflow, agents (especially workers like spec writers, architects, coders with TDD, and dedicated documentation writers) produce human-readable artifacts (plans, specifications, architectural documents, code, test reports, final documentation) *as specified by the [`01_AI-RUN/`](01_AI-RUN/) scripts*. The `✍️ @orchestrator-pheromone-scribe`, through its interpretation of summaries, populates a `documentationRegistry` within the [`.pheromone`](.pheromone:1) file. This registry tracks these vital documents, making project progress, decisions, and potential issues transparent and understandable to human supervisors and developers.

## 🏛️ System Architecture: Agents & Key Files Executing the [`01_AI-RUN/`](01_AI-RUN/) Workflow

Pheromind's architecture revolves around specialized AI agents that execute the workflow defined in [`01_AI-RUN/`](01_AI-RUN/) scripts, a central state file ([`.pheromone`](.pheromone:1)) managed by the Scribe reflecting this execution, and a configuration file ([`.swarmConfig`](.swarmConfig:1)) guiding the Scribe's interpretation of progress.

### Key Files:
1.  **The [`.pheromone`](.pheromone:1) File: The Swarm's Shared Understanding & Documentation Hub**
    This single JSON file, exclusively managed by the `✍️ @orchestrator-pheromone-scribe`, acts as the central repository for the swarm's current interpreted state and documentation pointers, reflecting the progress of the [`01_AI-RUN/`](01_AI-RUN/) workflow. It contains two primary top-level keys:
    *   **`signals`**: An array of structured JSON `:signal` objects representing the current "pheromone landscape."
    *   **`documentationRegistry`**: A JSON object mapping to and describing key human-readable project documents (specifications, architecture, plans, reports – often outputs of [`01_AI-RUN/`](01_AI-RUN/) phases), essential for human oversight and agent context.
    The Scribe *never* writes configuration data (from [`.swarmConfig`](.swarmConfig:1) or [`.roomodes`](.roomodes:1)) into this file.
    *   **Relationship with `project_session_state.json`:** If the executed [`01_AI-RUN/`](01_AI-RUN/) workflow (e.g., as defined in [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1)) mentions a `project_session_state.json` file, it should be understood that for Pheromind's operation, the [`.pheromone`](.pheromone:1) file is the **primary and authoritative state management mechanism**. The `project_session_state.json` might be a legacy concept from the original workflow definition, an intermediate output of a specific [`01_AI-RUN/`](01_AI-RUN/) phase if still generated (and in such cases, its path would be tracked in the `documentationRegistry`), or its role is superseded and augmented by the more dynamic and comprehensive [`.pheromone`](.pheromone:1) file. Pheromind agents rely on [`.pheromone`](.pheromone:1) for their state awareness and decision-making.

2.  **The [`.swarmConfig`](.swarmConfig:1) File: The Scribe's Interpretation Rulebook**
    A separate JSON file (e.g., `project_root/.swarmConfig`) containing all operational parameters for signal dynamics and, most importantly, the **`interpretationLogic`**. This logic (rules, patterns, semantic mappings) dictates how the `✍️ @orchestrator-pheromone-scribe` translates incoming natural language summaries (reporting on [`01_AI-RUN/`](01_AI-RUN/) phase completions) into structured `:signals` and `documentationRegistry` updates. The Scribe loads this file at the start of its cycle and *never* modifies it.

3.  **The [`.roomodes`](.roomodes:1) File: Agent Definitions**
    This file contains the JSON definitions for all Pheromind agents, detailing their roles, specific instructions (`customInstructions`), and capabilities, enabling them to execute tasks within the [`01_AI-RUN/`](01_AI-RUN/) workflow.

### Core Agents:
1.  **`✍️ @orchestrator-pheromone-scribe` (The Pheromone Scribe)**
    The intelligent gatekeeper and *sole manipulator* of the [`.pheromone`](.pheromone:1) file.
    *   Loads `interpretationLogic` from the [`.swarmConfig`](.swarmConfig:1) file.
    *   Loads the current [`.pheromone`](.pheromone:1) file (or bootstraps an empty one: `{"signals": [], "documentationRegistry": {}}` if it doesn't exist on its first run).
    *   Receives comprehensive natural language summaries and handoff reason codes from Task Orchestrators (or the `🧐 @uber-orchestrator` if it directly managed a worker for an [`01_AI-RUN/`](01_AI-RUN/) phase), reporting on [`01_AI-RUN/`](01_AI-RUN/) phase execution.
    *   **Interprets** this NL summary using its `interpretationLogic` to understand completed work, AI-verifiable outcomes, new needs, problems, and generated documentation as per the [`01_AI-RUN/`](01_AI-RUN/) workflow.
    *   **Generates/Updates** structured JSON `:signals` in the `signals` array and entries in the `documentationRegistry`.
    *   Manages signal dynamics (evaporation, amplification, pruning) applied *only* to signals, as defined in [`.swarmConfig`](.swarmConfig:1).
    *   Persists the updated `signals` and `documentationRegistry` to the [`.pheromone`](.pheromone:1) file.
    *   Activates the `🎩 @head-orchestrator` to continue the project flow according to the [`01_AI-RUN/`](01_AI-RUN/) sequence.

2.  **`🎩 @head-orchestrator` (Plan Custodian Initiator)**
    Initiates the project by passing its initial prompt (which includes details of the [`01_AI-RUN/`](01_AI-RUN/) entry-point script and essential path parameters) directly to the `🧐 @uber-orchestrator`.

3.  **`🧐 @uber-orchestrator` (Pheromone-Guided Delegator & [`01_AI-RUN/`](01_AI-RUN/) Workflow Executor)**
    The primary strategic decision-maker, responsible for driving the project according to the provided [`01_AI-RUN/`](01_AI-RUN/) entry-point script, guided by its "01_AI-RUN Workflow Orchestration" `customInstructions` in [`.roomodes`](.roomodes:1).
    *   **State & Documentation Awareness:** Reads the [`.pheromone`](.pheromone:1) file (signals and `documentationRegistry`) and consults referenced documents (often outputs of previous [`01_AI-RUN/`](01_AI-RUN/) phases) to understand the global project state and ensure human programmer clarity.
    *   **Strategic Delegation based on [`01_AI-RUN/`](01_AI-RUN/):** Based on the objectives and sequence defined in the current [`01_AI-RUN/`](01_AI-RUN/) script (e.g., [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1) orchestrating other phase scripts like [`01_AI-RUN/03_Idea.md`](01_AI-RUN/03_Idea.md:1)), and the current "pheromone landscape," it determines the next `01_AI-RUN` phase. It then identifies the corresponding `01_AI-RUN/*.md` sub-prompt and delegates its execution to the appropriate **Task-Specific Orchestrator** or directly to a **Worker Agent** as specified in its "01_AI-RUN Workflow Orchestration" logic.
    *   **Ensuring AI-Verifiable Tasks (as per [`01_AI-RUN/`](01_AI-RUN/)):** Crucially, it instructs selected Task Orchestrators (or Worker Agents) to execute tasks with clear, AI-verifiable end results *as specified or implied by the [`01_AI-RUN/`](01_AI-RUN/) scripts*. It also tells them to consult the [`.pheromone`](.pheromone:1) file and relevant documents (often outputs of prior [`01_AI-RUN/`](01_AI-RUN/) phases) for context.
    *   **Handles User Responses:** If a worker mode used `ask_followup_question` during an [`01_AI-RUN/`](01_AI-RUN/) phase, the `🧐 @uber-orchestrator` receives the user's response and passes it back to the worker mode that asked the question.

4.  **Task-Specific Orchestrators (e.g., `🌟 @orchestrator-sparc-specification-master-test-plan`, `🛠️ @orchestrator-framework-scaffolding`, `⚙️ @orchestrator-feature-implementation-tdd`, `✍️ @orchestrator-technical-documentation`)**
    Manage distinct, large-scale project phases as defined by the [`01_AI-RUN/`](01_AI-RUN/) workflow (when tasked by the `🧐 @uber-orchestrator`), enforcing AI-verifiable outcomes.
    *   **Phase Management with Verifiability (Following [`01_AI-RUN/`](01_AI-RUN/)):** Decompose their assigned [`01_AI-RUN/`](01_AI-RUN/) phase into logical sub-tasks, each with an AI-verifiable end result (e.g., `🌟 @orchestrator-sparc-specification-master-test-plan`, when directed by an [`01_AI-RUN/`](01_AI-RUN/) script, creates a Master Project Plan where every task has an AI-verifiable deliverable).
    *   **Worker Delegation (AI-Verifiable, as per [`01_AI-RUN/`](01_AI-RUN/)):** Assign sub-tasks to specialized Worker Agents, providing them with instructions derived from the [`01_AI-RUN/`](01_AI-RUN/) script that define AI-verifiable completion criteria.
    *   **Synthesis of Outcomes:** Collect rich natural language `Summary` reports (detailing verifiable results of [`01_AI-RUN/`](01_AI-RUN/) tasks) from workers. Synthesize these, plus their own phase management narrative, into a *single, comprehensive natural language summary*.
    *   **Reporting to Scribe:** Send this comprehensive NL summary and a handoff reason code to the `✍️ @orchestrator-pheromone-scribe` for interpretation. They *do not* generate structured `:signals`. Their summary must explain its intent for Scribe interpretation based on `swarmConfig.interpretationLogic`. They also pass through original directive details (like the path to the current [`01_AI-RUN/`](01_AI-RUN/) script) to the Scribe.

5.  **Worker Agents (e.g., `👨‍💻 @coder-test-driven`, `📝 @spec-writer-feature-overview`, `🔎 @research-planner-strategic`, `🧪 @tester-tdd-master`, `🧐 @code-comprehension-assistant-v2`)**
    Specialists performing granular, hands-on tasks (defined by [`01_AI-RUN/`](01_AI-RUN/) scripts) that produce AI-verifiable results.
    *   **Focused Execution for Verifiable Outcomes (Following [`01_AI-RUN/`](01_AI-RUN/)):** Execute narrowly defined roles (e.g., write code to pass specific tests as per a testing script in [`01_AI-RUN/`](01_AI-RUN/), generate a spec document matching a schema defined in an [`01_AI-RUN/`](01_AI-RUN/) doc, run tests verifying AI-Actionable End Results from a Test Plan created via an [`01_AI-RUN/`](01_AI-RUN/) phase).
    *   **Rich Natural Language Reporting:** Primary output to their parent Task Orchestrator (or the `🧐 @uber-orchestrator`) is a detailed, natural language `Summary` in their `task_completion` message. This summary meticulously describes actions taken, AI-verifiable results achieved (and how they were verified according to the [`01_AI-RUN/`](01_AI-RUN/) script), files created/modified (which become part of the human-readable documentation trail, e.g., `idea_document.md`), issues, and potential next steps.
    *   Worker Agents *do not* create or propose structured `:signals`. Their narrative `Summary` is raw input for aggregation and eventual Scribe interpretation. The `🧪 @tester-tdd-master` is crucial for verifying AI-Verifiable End Results using London School TDD and recursive testing, as potentially outlined in an [`01_AI-RUN/`](01_AI-RUN/) testing phase script.

## 🚀 Getting Started with Pheromind: An Ultra-Detailed Guide

Initiating a Pheromind project to execute an [`01_AI-RUN/`](01_AI-RUN/) workflow involves a clear setup process, ensuring the swarm has the necessary configuration and initial directive to begin its autonomous work. This guide walks you through each step.

**Phase 1: Foundational Setup - Equipping the Swarm**

1.  **Environment Configuration:**
    *   Ensure you have a compatible Roo Code environment operational.
    *   Configure your chosen Large Language Model (LLM), such as Claude 3.x, ensuring API keys are correctly set up and accessible.

2.  **Define Agent Behaviors: The [`.roomodes`](.roomodes:1) File:**
    *   This JSON file is the blueprint for your AI agents. Each entry defines an agent's role, specialized instructions (`custom_instructions`), and capabilities.
    *   Carefully craft or review the definitions for core agents like the `✍️ @orchestrator-pheromone-scribe`, `🎩 @head-orchestrator`, `🧐 @uber-orchestrator` (especially its "01_AI-RUN Workflow Orchestration" logic), various Task-Specific Orchestrators, and Worker Agents.
    *   Place this file in your project root (e.g., `/your_project_root/.roomodes`).

3.  **Establish the Scribe's Rulebook: The [`.swarmConfig`](.swarmConfig:1) File:**
    *   This JSON file is **critical** and *must be created by the user* in the project root (e.g., `/your_project_root/.swarmConfig`). The `✍️ @orchestrator-pheromone-scribe` relies entirely on this file for its operational logic.
    *   **`interpretationLogic` (The Core):** This is the most vital section. It contains a structured set of rules, patterns, keywords, and semantic mappings. The Scribe uses this logic to:
        *   Parse the natural language summaries received from Task Orchestrators (reporting on [`01_AI-RUN/`](01_AI-RUN/) phase execution).
        *   Identify key events, AI-verifiable outcomes, newly created documents (as per [`01_AI-RUN/`](01_AI-RUN/) outputs), problems, and needs.
        *   Translate this understanding into structured JSON `:signals`.
        *   Determine which documents to add or update in the `documentationRegistry`.
        *   *Example*: `interpretationLogic` might define that phrases like "Execution of `01_AI-RUN/03_Idea.md` complete, `idea_document.md` created at..." or "All tests passed for feature X as per `01_AI-RUN/10_Testing.md`" trigger specific `signalType` generation and `documentationRegistry` entries.
    *   **Signal Dynamics:** Define parameters like:
        *   `evaporationRates`: How quickly signals lose strength over time.
        *   `amplificationRules`: Conditions under which signal strength increases.
        *   `pruningThresholds`: Rules for removing weak or old signals.
        *   `signalPriorities`: Relative importance of different signal types.
    *   **Signal Definitions:** List valid `signalTypes`, `category` definitions, and expected `data` schemas for different signals.
    *   The Scribe loads [`.swarmConfig`](.swarmConfig:1) at the beginning of each operational cycle and *never modifies it*. A well-defined [`.swarmConfig`](.swarmConfig:1) is essential for coherent swarm behavior and accurate state tracking of the [`01_AI-RUN/`](01_AI-RUN/) workflow.

4.  **Prepare the Swarm's Memory: The [`.pheromone`](.pheromone:1) File (Initial State):**
    *   This JSON file, typically located at `project_root/.pheromone`, stores the swarm's collective, interpreted state of the [`01_AI-RUN/`](01_AI-RUN/) workflow execution.
    *   **Bootstrapping by the Scribe:** For a brand-new project, you *do not need to manually create this file*. On its very first run, if the `✍️ @orchestrator-pheromone-scribe` detects that the [`.pheromone`](.pheromone:1) file (as specified by its `Pheromone_File_Path` parameter) is missing, it will automatically **bootstrap** an empty one with the following structure:
        ```json
        {
          "signals": [],
          "documentationRegistry": {}
        }
        ```
    *   For subsequent runs, the Scribe loads the existing [`.pheromone`](.pheromone:1) file and updates it.

**Phase 2: Providing the Initial [`01_AI-RUN/`](01_AI-RUN/) Directive**

5.  **Identify Your [`01_AI-RUN/`](01_AI-RUN/) Entry-Point Script:**
    *   This is typically a script like [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1) which orchestrates the sequence of other [`01_AI-RUN/`](01_AI-RUN/) phase scripts, or a specific phase script like [`01_AI-RUN/01_Getting_Started.md`](01_AI-RUN/01_Getting_Started.md:1) if you intend to start from a particular point.
    *   This script will serve as the initial high-level plan for Pheromind to execute.

**Phase 3: Initiating the Swarm - The First "Boomerang" to Execute an [`01_AI-RUN/`](01_AI-RUN/) Phase**

6.  **Activate the `🎩 @head-orchestrator` with an [`01_AI-RUN/`](01_AI-RUN/) Entry Point:**
    *   This is the user's primary action to kickstart the Pheromind workflow, directing it to execute a specific sequence from the [`01_AI-RUN/`](01_AI-RUN/) directory.
    *   When activating the `🎩 @head-orchestrator`, you **must** provide it with specific parameters. These parameters are crucial for the entire swarm to locate resources and understand the project context. The typical essential parameters are:
        *   **`Original_User_Directive_Type_Field`**: A string indicating the nature of the input, often `"AI_RUN_Workflow_Execution"` or similar when pointing to an [`01_AI-RUN/`](01_AI-RUN/) script.
        *   **`Original_User_Directive_Payload_Path_Field`**: The **absolute or relative path** to the entry-point script within the [`01_AI-RUN/`](01_AI-RUN/) directory (e.g., `"01_AI-RUN/02_AutoPilot.md"` or `"01_AI-RUN/01_Getting_Started.md"`). This script defines the high-level project plan or the initial phase to be executed.
        *   **`Original_Project_Root_Path_Field`**: The **absolute path** to your project's root directory (e.g., `"/Users/username/dev/MyPheromindProject"`). This allows all agents to correctly resolve file paths.
        *   **`Pheromone_File_Path`**: The **absolute or relative path** to the [`.pheromone`](.pheromone:1) file (e.g., `".pheromone"` or `"config/.pheromone"` if relative to project root, or an absolute path). Both the `🧐 @uber-orchestrator` and the `✍️ @orchestrator-pheromone-scribe` will use this path.

7.  **The Initial Handoff and First Cycle (Executing the [`01_AI-RUN/`](01_AI-RUN/) Script):**
    *   The `🎩 @head-orchestrator` takes the provided parameters, including the path to the entry-point [`01_AI-RUN/`](01_AI-RUN/) script.
    *   It immediately passes this information to the `🧐 @uber-orchestrator`.
    *   The `🧐 @uber-orchestrator` now takes charge of executing the specified [`01_AI-RUN/`](01_AI-RUN/) workflow, following its "01_AI-RUN Workflow Orchestration" logic from [`.roomodes`](.roomodes:1):
        *   It reads the (potentially newly bootstrapped) [`.pheromone`](.pheromone:1) file using the `Pheromone_File_Path` to check for the last completed `01_AI-RUN` phase.
        *   It accesses and interprets the entry-point [`01_AI-RUN/`](01_AI-RUN/) script (e.g., [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1)) using the `Original_User_Directive_Payload_Path_Field` and `Original_Project_Root_Path_Field`. This script serves as its high-level plan.
        *   The `🧐 @uber-orchestrator` then determines the next `01_AI-RUN` phase based on the defined sequence (Getting Started -> Idea -> Market Research, etc.) and identifies the corresponding `01_AI-RUN/*.md` sub-prompt.
        *   It delegates the execution of this phase/sub-prompt to the appropriate specialized agent (e.g., `🧐 @code-comprehension-assistant-v2` for 'Getting Started' with [`01_AI-RUN/01_Getting_Started.md`](01_AI-RUN/01_Getting_Started.md:1), `🔎 @research-planner-strategic` for 'Idea' with [`01_AI-RUN/03_Idea.md`](01_AI-RUN/03_Idea.md:1)). The goal is to achieve the AI-verifiable outcomes specified in the [`01_AI-RUN/`](01_AI-RUN/) script for the current phase.
    *   Once a phase defined in an [`01_AI-RUN/`](01_AI-RUN/) script is completed (e.g., `idea_document.md` created as per [`01_AI-RUN/03_Idea.md`](01_AI-RUN/03_Idea.md:1)), the responsible Task Orchestrator (or worker, if directly tasked by `🧐 @uber-orchestrator`) compiles a comprehensive natural language summary.
    *   This summary is sent to the `✍️ @orchestrator-pheromone-scribe`. The Scribe, using `interpretationLogic` from [`.swarmConfig`](.swarmConfig:1), updates `:signals` and the `documentationRegistry` in [`.pheromone`](.pheromone:1) to reflect the completed [`01_AI-RUN/`](01_AI-RUN/) phase and its outputs.
    *   This completes the first full "boomerang" cycle for that phase of the [`01_AI-RUN/`](01_AI-RUN/) workflow, and the [`.pheromone`](.pheromone:1) file is updated, ready to guide the next phase as defined in the [`01_AI-RUN/`](01_AI-RUN/) sequence.

8.  **Observe, Iterate, and Supervise:**
    *   Monitor the logs generated by the agents to understand their actions and decisions as they execute the [`01_AI-RUN/`](01_AI-RUN/) workflow.
    *   Inspect the [`.pheromone`](.pheromone:1) file (in a read-only manner) to see how signals and the `documentationRegistry` evolve with each completed [`01_AI-RUN/`](01_AI-RUN/) phase.
    *   Review the documents created by the agents (e.g., `idea_document.md`, `project_prd.md`), as listed in the `documentationRegistry`.
    *   Pheromind is designed for autonomy in executing the [`01_AI-RUN/`](01_AI-RUN/) workflow, but human oversight is valuable for ensuring alignment and making high-level adjustments if needed (typically by providing new directives or refining [`.swarmConfig`](.swarmConfig:1) or the [`01_AI-RUN/`](01_AI-RUN/) scripts themselves).

By following these steps, you can successfully launch a Pheromind project to execute a predefined [`01_AI-RUN/`](01_AI-RUN/) workflow, leveraging its autonomous capabilities to manage and execute complex tasks based on AI-verifiable outcomes.

## 🔄 The Pheromind Project Lifecycle: Executing the [`01_AI-RUN/`](01_AI-RUN/) Workflow with AI-Verifiable Outcomes

Pheromind's power lies in its adaptable, cyclical workflow, designed to execute predefined project sequences like those in the [`01_AI-RUN/`](01_AI-RUN/) directory. This "boomerang task" lifecycle ensures that every step, as dictated by the [`01_AI-RUN/`](01_AI-RUN/) scripts, is guided by the collective intelligence of the swarm, its state recorded in the [`.pheromone`](.pheromone:1) file, and its outputs validated by AI-verifiable outcomes. Here’s an ultra-detailed look at how Pheromind executes such a workflow:

**Core Principle: The AI-Verifiable "Boomerang Task" Executing [`01_AI-RUN/`](01_AI-RUN/) Phases**

The entire Pheromind workflow revolves around a "boomerang" pattern applied to the execution of [`01_AI-RUN/`](01_AI-RUN/) scripts:
1.  **Delegation Downwards (Following [`01_AI-RUN/`](01_AI-RUN/)):** Tasks defined in an [`01_AI-RUN/`](01_AI-RUN/) script are broken down and delegated by the `🧐 @uber-orchestrator` (or Task-Specific Orchestrators if used as intermediaries) to more specialized agents. Each delegation includes clear **AI-verifiable completion criteria** as specified or implied by the [`01_AI-RUN/`](01_AI-RUN/) script for that phase.
2.  **Execution & Verification (As per [`01_AI-RUN/`](01_AI-RUN/)):** Worker agents execute their tasks, focusing on achieving these verifiable outcomes and producing the deliverables outlined in the guiding [`01_AI-RUN/`](01_AI-RUN/) script (e.g., creating `idea_document.md` when executing the logic of [`01_AI-RUN/03_Idea.md`](01_AI-RUN/03_Idea.md:1)).
3.  **Reporting Upwards:** Results, including confirmation of AI-verified outcomes and paths to deliverables (e.g., the path to the newly created `idea_document.md`), are reported back up the chain as rich **natural language summaries**.
4.  **Interpretation & State Update:** The `✍️ @orchestrator-pheromone-scribe` interprets these aggregated summaries, updating the central [`.pheromone`](.pheromone:1) file (both `:signals` and `documentationRegistry`) to reflect the completion of the [`01_AI-RUN/`](01_AI-RUN/) phase and register its outputs.
5.  **Adaptive Next Cycle (Progressing through [`01_AI-RUN/`](01_AI-RUN/)):** The updated [`.pheromone`](.pheromone:1) state guides the next cycle of delegation and execution, moving to the subsequent phase or script in the [`01_AI-RUN/`](01_AI-RUN/) sequence.

**The Detailed Project Lifecycle Phases (Executing an [`01_AI-RUN/`](01_AI-RUN/) Workflow):**

**Phase 0: Foundational Setup & Initiation (As detailed in "Getting Started")**
*   The user provides an initial directive, typically the path to an entry-point script in the [`01_AI-RUN/`](01_AI-RUN/) directory (e.g., [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1)), and necessary path parameters to the `🎩 @head-orchestrator`.
*   The `🎩 @head-orchestrator` passes this to the `🧐 @uber-orchestrator`.
*   The `✍️ @orchestrator-pheromone-scribe` bootstraps [`.pheromone`](.pheromone:1) if it doesn't exist.
*   **`🧐 @uber-orchestrator`'s Initial Action (e.g., "Getting Started"):**
    *   The `🧐 @uber-orchestrator` reads the entry-point [`01_AI-RUN/`](01_AI-RUN/) script (e.g., [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1)) and the (potentially empty) [`.pheromone`](.pheromone:1) file.
    *   Following its "01_AI-RUN Workflow Orchestration" logic, it determines the first phase is 'Getting Started'.
    *   It tasks `🧐 @code-comprehension-assistant-v2` with the [`01_AI-RUN/01_Getting_Started.md`](01_AI-RUN/01_Getting_Started.md:1) sub-prompt, providing [`02_AI-DOCS/Documentation/Codebase_Xray_Prompt.md`](02_AI-DOCS/Documentation/Codebase_Xray_Prompt.md:1) as a guide and specifying `03_SPECS/codebase_xray_analysis.json` as the output.
    *   The `🧐 @code-comprehension-assistant-v2` executes, produces `03_SPECS/codebase_xray_analysis.json`, and reports its summary.
    *   This summary is passed to the `✍️ @orchestrator-pheromone-scribe`, which updates [`.pheromone`](.pheromone:1) (signals and `documentationRegistry`).

**Phase 1 onwards: Iteratively Executing the Remainder of the [`01_AI-RUN/`](01_AI-RUN/) Workflow (e.g., Idea, Market Research, PRD, etc.)**

This process continues cyclically, with the `🧐 @uber-orchestrator` driving the execution of each subsequent script/phase defined in the [`01_AI-RUN/`](01_AI-RUN/) sequence (e.g., Idea via [`01_AI-RUN/03_Idea.md`](01_AI-RUN/03_Idea.md:1), Market Research via [`01_AI-RUN/04_Market_Research.md`](01_AI-RUN/04_Market_Research.md:1), PRD Generation via [`01_AI-RUN/06_PRD_Generation.md`](01_AI-RUN/06_PRD_Generation.md:1), etc.).

1.  **Strategic Delegation by `🧐 @uber-orchestrator` (Following [`01_AI-RUN/`](01_AI-RUN/) and [`.roomodes`](.roomodes:1)):**
    *   The `🎩 @head-orchestrator` re-engages the `🧐 @uber-orchestrator` (after the Scribe's update).
    *   The `🧐 @uber-orchestrator` consults the *updated* [`.pheromone`](.pheromone:1] file. The current `:signals` and `documentationRegistry` (which now includes outputs from previous [`01_AI-RUN/`](01_AI-RUN/) phases like `codebase_xray_analysis.json`) guide its decision.
    *   Following its "01_AI-RUN Workflow Orchestration" logic, it determines the next phase (e.g., 'Idea').
    *   It identifies the corresponding sub-prompt (e.g., [`01_AI-RUN/03_Idea.md`](01_AI-RUN/03_Idea.md:1)) and the designated agent (e.g., `🔎 @research-planner-strategic`).
    *   It tasks `🔎 @research-planner-strategic` with [`01_AI-RUN/03_Idea.md`](01_AI-RUN/03_Idea.md:1), `phase_type: 'IdeaGeneration'`, and output path `02_AI-DOCS/Project_Brief/idea_document.md`.
    *   **Mandate:** The agent must adhere to the instructions and AI-verifiable outcomes specified in that particular [`01_AI-RUN/`](01_AI-RUN/) script.

2.  **Worker Agent Execution (Executing an [`01_AI-RUN/`](01_AI-RUN/) Script's Content):**
    *   The assigned Worker Agent (e.g., `🔎 @research-planner-strategic`) consults the relevant [`01_AI-RUN/`](01_AI-RUN/) script (e.g., [`01_AI-RUN/03_Idea.md`](01_AI-RUN/03_Idea.md:1)) and any prerequisite documents listed in the `documentationRegistry`.
    *   It executes the tasks outlined in the [`01_AI-RUN/`](01_AI-RUN/) script.
    *   *Example (Idea Generation based on [`01_AI-RUN/03_Idea.md`](01_AI-RUN/03_Idea.md:1)):*
        *   `🔎 @research-planner-strategic` uses instructions in [`01_AI-RUN/03_Idea.md`](01_AI-RUN/03_Idea.md:1) to generate `idea_document.md`.
        *   AI-verifiable outcome: `idea_document.md` created and populated according to [`01_AI-RUN/03_Idea.md`](01_AI-RUN/03_Idea.md:1).
        *   If user validation is required (as per [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1)), the worker uses `ask_followup_question`. The response is routed back via the `🧐 @uber-orchestrator` for the worker to incorporate.

3.  **Worker Reporting & AI-Verified Output (As per [`01_AI-RUN/`](01_AI-RUN/)):**
    *   The Worker Agent produces its deliverable as specified by the script.
    *   It generates a detailed natural language `Summary` confirming its AI-verifiable outcome (e.g., "Idea generation complete as per [`01_AI-RUN/03_Idea.md`](01_AI-RUN/03_Idea.md:1). Output at `02_AI-DOCS/Project_Brief/idea_document.md`.").
    *   This summary is sent to the `🧐 @uber-orchestrator` (or its designated Task Orchestrator).

4.  **Handoff to Scribe & State Evolution:**
    *   The `🧐 @uber-orchestrator` (or Task Orchestrator) forwards the comprehensive NL summary to the `✍️ @orchestrator-pheromone-scribe`.
    *   The Scribe interprets it, updates `:signals` (e.g., `ai_run_phase_idea_generation_complete_verified`), and adds the new output (e.g., `idea_document.md`) to the `documentationRegistry` in [`.pheromone`](.pheromone:1).
    *   The Scribe activates the `🎩 @head-orchestrator`.

5.  **Cycle Continuation & Adaptation (Through the [`01_AI-RUN/`](01_AI-RUN/) Workflow):**
    *   The `🎩 @head-orchestrator` re-engages the `🧐 @uber-orchestrator`.
    *   The `🧐 @uber-orchestrator` reads the *newly updated* [`.pheromone`](.pheromone:1] and proceeds to the next phase in the [`01_AI-RUN/`](01_AI-RUN/) sequence (e.g., Market Research, then PRD Generation, etc.), delegating to the appropriate agents as per its "01_AI-RUN Workflow Orchestration" logic.
    *   **Adaptability:** If an [`01_AI-RUN/`](01_AI-RUN/) script execution signals an error, the `🧐 @uber-orchestrator` might delegate to a `🪲 @debugger-targeted` or re-attempt the script with modified parameters if the script allows. The primary goal is to complete the defined [`01_AI-RUN/`](01_AI-RUN/) workflow.

**Subsequent Phases (Specs & Docs, Task Management, Implementation, Testing, Deployment):**
*   Pheromind continues to execute the phases as defined by the corresponding [`01_AI-RUN/`](01_AI-RUN/) scripts (e.g., [`01_AI-RUN/07_Specs_Docs.md`](01_AI-RUN/07_Specs_Docs.md:1), [`01_AI-RUN/09_Task_Manager.md`](01_AI-RUN/09_Task_Manager.md:1), [`01_AI-RUN/08_Start_Building.md`](01_AI-RUN/08_Start_Building.md:1), [`01_AI-RUN/10_Testing.md`](01_AI-RUN/10_Testing.md:1), [`01_AI-RUN/11_Deployment.md`](01_AI-RUN/11_Deployment.md:1)).
*   For each phase, the relevant [`01_AI-RUN/*.md`](01_AI-RUN/) script provides the "what" and "sequence," and Pheromind agents (tasked by the `🧐 @uber-orchestrator` as per [`.roomodes`](.roomodes:1)) provide the "how," ensuring AI-verifiable outcomes are met and documented in the `documentationRegistry` within [`.pheromone`](.pheromone:1).
*   For example, during the "Specs & Docs" phase (driven by [`01_AI-RUN/07_Specs_Docs.md`](01_AI-RUN/07_Specs_Docs.md:1)), the `🧐 @uber-orchestrator` tasks the `✍️ @orchestrator-technical-documentation` mode. This orchestrator then manages the creation of project-specific documents (e.g., `architecture.md`, `coding_conventions.md`) in the `02_AI-DOCS/` and `03_SPECS/` directories by instructing worker agents to copy and populate templates, as per [`01_AI-RUN/07_Specs_Docs.md`](01_AI-RUN/07_Specs_Docs.md:1). These created documents are then registered in [`.pheromone`](.pheromone:1).
*   User validation points, as defined in scripts like [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1), are handled by worker agents using the `ask_followup_question` tool. Responses are routed back via the `🧐 @uber-orchestrator` to the originating worker, allowing for user feedback to be incorporated before finalizing phase deliverables.

**Executing "Anything" with Pheromind (by following [`01_AI-RUN/`](01_AI-RUN/)):**

Pheromind's ability to execute "anything" is derived from its role as an engine for structured workflows like [`01_AI-RUN/`](01_AI-RUN/):
*   **Flexibility of [`01_AI-RUN/`](01_AI-RUN/) Scripts:** The [`01_AI-RUN/`](01_AI-RUN/) scripts can define any sequence of tasks and AI-verifiable outcomes suitable for any project type.
*   **Specialized Worker Agents:** The [`.roomodes`](.roomodes:1) file allows defining agents with skills to execute the specific tasks detailed in the [`01_AI-RUN/`](01_AI-RUN/) scripts.
*   **Configurable `interpretationLogic`:** The [`.swarmConfig`](.swarmConfig:1) allows the Scribe to understand progress indicators relevant to the specific [`01_AI-RUN/`](01_AI-RUN/) workflow being executed.
*   **The [`01_AI-RUN/`](01_AI-RUN/) Workflow as the Master Plan:** The sequence of [`01_AI-RUN/`](01_AI-RUN/) scripts, often orchestrated by an entry script like [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1) and executed by the `🧐 @uber-orchestrator`, serves as the master plan that Pheromind executes.

The `documentationRegistry` in [`.pheromone`](.pheromone:1) plays a crucial role throughout, acting as a living library of the project's knowledge generated by executing the [`01_AI-RUN/`](01_AI-RUN/) workflow. It's not just for humans; agents (especially orchestrators and the `🧐 @uber-orchestrator`) consult these documents (e.g., `project_prd.md`, `architecture.md` created as per [`01_AI-RUN/`](01_AI-RUN/) instructions) to gain context for their tasks, ensuring decisions are informed by the latest outputs of the ongoing workflow. This makes the entire process robust, transparent, and adaptable.

## 🌟 Key Features & Capabilities

*   **Execution Engine for [`01_AI-RUN/`](01_AI-RUN/) Workflows:** Pheromind is designed to interpret and execute structured project workflows like those defined in the [`01_AI-RUN/`](01_AI-RUN/) directory.
*   **AI-Verifiable Project Execution:** Ensures progress through the [`01_AI-RUN/`](01_AI-RUN/) workflow is tracked via concrete, measurable, and AI-confirmable outcomes.
*   **Autonomous Project Management:** Manages complex lifecycles defined in [`01_AI-RUN/`](01_AI-RUN/) scripts with minimal human intervention post-initiation, driven by the `🧐 @uber-orchestrator`.
*   **Human-Centric Documentation Trail:** Actively tracks and registers human-readable documents (outputs of [`01_AI-RUN/`](01_AI-RUN/) phases) via the `documentationRegistry` in [`.pheromone`](.pheromone:1) for transparency and oversight.
*   **Sophisticated NL-Driven State Updates:** The `✍️ @orchestrator-pheromone-scribe` translates rich narrative summaries (reporting on [`01_AI-RUN/`](01_AI-RUN/) execution) into structured state (`:signals`) and documentation links, guided by [`.swarmConfig`](.swarmConfig:1).
*   **Dynamic & Adaptive Tasking:** Evolves project direction based on real-time, interpreted state from the [`.pheromone`](.pheromone:1) file, while adhering to the [`01_AI-RUN/`](01_AI-RUN/) sequence.
*   **Resilience & Modularity:** Decentralized coordination and clear role specialization (defined in [`.roomodes`](.roomodes:1)) promote robustness in executing the [`01_AI-RUN/`](01_AI-RUN/) workflow.
*   **Centralized State Interpretation:** The `✍️ @orchestrator-pheromone-scribe`'s exclusive management of [`.pheromone`](.pheromone:1) ensures coherent state updates reflecting [`01_AI-RUN/`](01_AI-RUN/) progress.

## 💡 Why Pheromind? The Design Philosophy

*   **Verifiable Progress through Workflow Execution:** Pheromind isn't just about doing tasks; it's about *proving* they're done correctly by executing a defined workflow (like [`01_AI-RUN/`](01_AI-RUN/)) with AI-verifiable criteria at each step.
*   **The Power of Interpreted Narratives:** Leverages natural language for rich communication about workflow progress, with the Scribe performing the heavy lifting of translation into formal state based on [`.swarmConfig`](.swarmConfig:1). This allows flexibility and expressiveness beyond rigid message formats.
*   **Stigmergy for Scalable Coordination:** Indirect communication via the [`.pheromone`](.pheromone:1) medium enables adaptability and scalability in executing complex, multi-phase workflows.
*   **Centralized Interpretation, Decentralized Action:** The `✍️ @orchestrator-pheromone-scribe` centralizes state interpretation for consistency, while agents act with role-specific autonomy to fulfill the objectives of the [`01_AI-RUN/`](01_AI-RUN/) scripts.
*   **Emergent Behavior Guided by Explicit Logic:** Complex project management emerges from agent interactions governed by defined roles ([`.roomodes`](.roomodes:1)), the Scribe's explicit `interpretationLogic` ([`.swarmConfig`](.swarmConfig:1)), and the overarching structure of the [`01_AI-RUN/`](01_AI-RUN/) workflow.
*   **Transparency and Human Oversight:** AI-verifiable outcomes and a maintained `documentationRegistry` provide clear insight into the swarm's operations as it executes the [`01_AI-RUN/`](01_AI-RUN/) plan.

## 🧬 The Pheromone Ecosystem: [`.pheromone`](.pheromone:1), [`.swarmConfig`](.swarmConfig:1), and [`.roomodes`](.roomodes:1)

These three components are crucial for Pheromind to execute the [`01_AI-RUN/`](01_AI-RUN/) workflow:

### 1. The [`.pheromone`](.pheromone:1) File
*   The swarm's interpreted shared state, exclusively written to by the `✍️ @orchestrator-pheromone-scribe`, reflecting the current status of the [`01_AI-RUN/`](01_AI-RUN/) workflow.
*   Contains:
    *   `signals`: An array of structured JSON `:signal` objects.
        ```json
        // Example Signal in .pheromone's "signals" array
        {
          "id": "signal-xyz-789",
          "signalType": "ai_run_phase_market_research_complete_verified",
          "target": "01_AI-RUN/04_Market_Research.md",
          "category": "workflow_phase_status_verified",
          "strength": 9.8,
          "message": "Execution of 01_AI-RUN/04_Market_Research.md complete. market_research_report.md generated and validated. Ready for Core Concept Definition phase.",
          "data": {
            "executedScript": "01_AI-RUN/04_Market_Research.md",
            "outputDocument": "02_AI-DOCS/Market_Analysis/market_research_report.md",
            "relevantDocRegistryKey": "doc_market_research_report_v1"
          },
          "timestamp_created": "2023-11-15T14:00:00Z",
          "last_updated_timestamp": "2023-11-15T14:00:00Z"
        }
        ```
    *   `documentationRegistry`: A JSON object mapping keys to metadata about project documents (path, description, timestamp), enabling human and AI access to critical information generated during the [`01_AI-RUN/`](01_AI-RUN/) workflow.
        ```json
        // Example entry in .pheromone's "documentationRegistry"
        "doc_idea_document_v1": {
          "path": "02_AI-DOCS/Project_Brief/idea_document.md",
          "description": "Initial project idea document generated as per 01_AI-RUN/03_Idea.md.",
          "lastUpdated": "2023-11-10T10:00:00Z",
          "generatedByAgentRole": "research-planner-strategic",
          "sourceAiRunScript": "01_AI-RUN/03_Idea.md"
        }
        ```

### 2. The [`.swarmConfig`](.swarmConfig:1) File
*   A separate JSON file defining the `✍️ @orchestrator-pheromone-scribe`'s "brain" and pheromone dynamics.
*   **Crucially contains `interpretationLogic`:** Rules, patterns, semantic mappings for the Scribe to parse NL summaries (reporting on [`01_AI-RUN/`](01_AI-RUN/) phase execution) and generate/update `:signals` and `documentationRegistry` entries.
*   Also defines `evaporationRates`, `amplificationRules`, `signalPriorities`, valid `signalTypes`, `category` definitions, etc.
*   Loaded by the Scribe; *never* modified by the Scribe. Careful tuning enables sophisticated emergent behavior in response to the [`01_AI-RUN/`](01_AI-RUN/) workflow.

### 3. The [`.roomodes`](.roomodes:1) File
*   Contains detailed JSON definitions for all AI agent modes, specifying their roles, `customInstructions` (including the `🧐 @uber-orchestrator`'s "01_AI-RUN Workflow Orchestration" logic), and capabilities, forming the behavioral blueprint of the swarm that executes the [`01_AI-RUN/`](01_AI-RUN/) workflow.

## ✍️ Crafting Effective Inputs: The [`01_AI-RUN/`](01_AI-RUN/) Entry-Point Script

High-quality initial input via the [`01_AI-RUN/`](01_AI-RUN/) entry-point script is key.
*   This script (e.g., [`01_AI-RUN/02_AutoPilot.md`](01_AI-RUN/02_AutoPilot.md:1)) should clearly define the sequence of project phases (often by referencing other [`01_AI-RUN/`](01_AI-RUN/) scripts) and their objectives.
*   Each phase script within the [`01_AI-RUN/`](01_AI-RUN/) directory should detail its specific tasks, expected outputs, and AI-verifiable outcomes.

The `✍️ @orchestrator-pheromone-scribe`'s interpretation of summaries derived from the execution of these [`01_AI-RUN/`](01_AI-RUN/) scripts will shape the signals and documentation registry, accurately reflecting project progress.

## (Optional) Contextual Terminology in `interpretationLogic`

The `swarmConfig.interpretationLogic` is powerful. Design it to recognize specific keywords, phrases, or patterns in Task Orchestrator (or `🧐 @uber-orchestrator`) summaries related to the execution of [`01_AI-RUN/`](01_AI-RUN/) scripts (e.g., "Execution of `01_AI-RUN/XYZ.md` complete," "Output `document.md` generated as per `01_AI-RUN/ABC.md`," "AI-verifiable outcome for phase `DEF` achieved"). The Scribe uses this to generate precise signals (e.g., `:ai_run_phase_XYZ_complete_verified`, `:document_ABC_output_registered`) and update the `documentationRegistry` accurately, enhancing swarm coordination and human understanding of the [`01_AI-RUN/`](01_AI-RUN/) workflow execution.

## 🤝 Contributing & Future Evolution

Pheromind is an evolving framework. We welcome contributions!
*(Standard contributing guidelines would go here.)*

**Potential Future Directions:**
*   Visual Pheromone & Documentation Landscape: Tools to visualize [`.pheromone`](.pheromone:1) signals and `documentationRegistry` in the context of the [`01_AI-RUN/`](01_AI-RUN/) workflow.
*   Advanced [`.swarmConfig`](.swarmConfig:1) Tuning & Validation UI.
*   Self-adaptive `interpretationLogic`: Scribe suggests improvements to its own rules based on [`01_AI-RUN/`](01_AI-RUN/) execution patterns.
*   Expanded Agent Ecosystem for diverse AI-verifiable project types defined in [`01_AI-RUN/`](01_AI-RUN/) scripts.
*   Enhanced Analytics on signal/documentation patterns for project health during [`01_AI-RUN/`](01_AI-RUN/) execution.