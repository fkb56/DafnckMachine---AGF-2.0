# Workflow Configuration and State Management

This document outlines the configuration and state management for the AI-Assisted Development Workflow.

## 1. Project Session State (`project_session_state.json`)

The [`project_session_state.json`](project_session_state.json:1) file is used to maintain the current state of the workflow. It should be located at the project root. The structure of this file is as follows:

```json
{
  "schemaVersion": "string",
  "projectName": "string",
  "projectType": "string",
  "projectObjective": "string",
  "currentWorkflowPhase": "string",
  "lastCompletedStep": "string",
  "pendingAction": "string | null",
  "errorState": {
    "hasError": "boolean",
    "errorMessage": "string | null",
    "recoverySuggestion": {
      "type": "string",
      "details": "string",
      "relevantFile": "string | null",
      "relevantStep": "string | null"
    }
  },
  "ideaDocumentPath": "string | null",
  "ideaDocumentLastValidatedHash": "string | null",
  "marketResearchReportPath": "string | null",
  "marketResearchReportLastValidatedHash": "string | null",
  "coreConceptPath": "string | null",
  "coreConceptLastValidatedHash": "string | null",
  "prdDocumentPath": "string | null",
  "prdDocumentLastValidatedHash": "string | null",
  "specsIndexPath": "string | null",
  "specsIndexLastValidatedHash": "string | null",
  "tasksDocumentPath": "string | null",
  "tasksDocumentLastValidatedHash": "string | null",
  "taskStatuses": {
    "taskId1": {
      "status": "string", // e.g., "todo", "inProgress", "Done", "Error"
      "lastUpdatedAt": "string" // ISO 8601 timestamp
    }
    // ... other tasks and their statuses
  },
  "warnings": [
    {
      "timestamp": "string", // ISO 8601 timestamp
      "sourcePhase": "string",
      "message": "string"
    }
    // ... other warnings
  ],
  "filenameMapping": {
    "logicalPhaseName": "actualFilename"
    // e.g., "ideaGeneration": "03_Idea.md",
    // "marketResearch": "04_Market_Research.md",
    // ... mapping for all phases
  }
}
```

### Field Descriptions:

-   `schemaVersion`: (string) Indicates the version of the `project_session_state.json` schema itself, to help manage structural changes to this state file over time. Example: "1.1.0".
-   `projectName`: (string) The name of the project.
-   `projectType`: (string) The main type of project (e.g., "React Web Application", "Node.js Backend API").
-   `projectObjective`: (string) A brief description of the project's goal.
-   `currentWorkflowPhase`: (string) The current phase of the workflow (e.g., "ideaGeneration", "marketResearch", "implementation").
-   `lastCompletedStep`: (string) A specific description of the last successfully completed step within the current phase.
-   `pendingAction`: (string | null) A description of an action that was interrupted, or `null` if no action is pending.
-   `errorState`: (object) An object containing information about a previous error, if any.
    -   `hasError`: (boolean) Boolean indicating if an error occurred.
    -   `errorMessage`: (string | null) Details of the error. Should be as specific as possible, ideally using predefined error type prefixes (e.g., "PromptFileNotFoundError:", "MCPToolFailure:", "StateUpdateError:", "MissingInputDocumentError:").
    -   `recoverySuggestion`: (object | null) An object detailing the suggested recovery action.
        -   `type`: (string) The type of recovery suggested (e.g., "retry_last_step", "skip_step", "user_clarification", "manual_intervention_required").
        -   `details`: (string) A detailed description of the suggested recovery action.
        -   `relevantFile`: (string, optional) Path to a file relevant to the error or recovery.
        -   `relevantStep`: (string, optional) The `lastCompletedStep` or specific action that failed.
-   `ideaDocumentPath`: (string | null) Path to the generated idea document.
-   `ideaDocumentLastValidatedHash`: (string, optional) Stores a hash (e.g., SHA256) of the idea document's content at the time of its last successful validation. This can be used to detect if a critical generated document has been modified externally or unexpectedly. Example: "sha256-a1b2c3d4..."
-   `marketResearchReportPath`: (string | null) Path to the generated market research report.
-   `marketResearchReportLastValidatedHash`: (string, optional) Hash of the market research report at last validation.
-   `coreConceptPath`: (string | null) Path to the generated core concept document.
-   `coreConceptLastValidatedHash`: (string, optional) Hash of the core concept document at last validation.
-   `prdDocumentPath`: (string | null) Path to the generated PRD.
-   `prdDocumentLastValidatedHash`: (string, optional) Hash of the PRD document at last validation.
-   `specsIndexPath`: (string | null) Path to the generated documentation index.
-   `specsIndexLastValidatedHash`: (string, optional) Hash of the specs index document at last validation.
-   `tasksDocumentPath`: (string | null) Path to the tasks JSON file.
-   `tasksDocumentLastValidatedHash`: (string, optional) Hash of the tasks document at last validation.
-   `taskStatuses`: (object) An object mapping task IDs to their current status details.
    -   For each `taskId`:
        -   `status`: (string) The current status of the task (e.g., "todo", "inProgress", "Done", "Error").
        -   `lastUpdatedAt`: (string) An ISO 8601 timestamp indicating when the status was last updated.
-   `warnings`: (array of objects, optional) An array to log non-critical warnings encountered during workflow execution that do not halt the process but may require user attention or indicate potential minor issues.
    -   Each warning object contains:
        -   `timestamp`: (string) ISO 8601 timestamp of when the warning was logged.
        -   `sourcePhase`: (string) The `currentWorkflowPhase` when the warning occurred.
        -   `message`: (string) The warning message (e.g., "Filename mapping fallback for 'LogicalPhaseName'.", "Persona not defined in sub-prompt X, proceeding with ProjectArchitect persona.").
-   `filenameMapping`: (object, optional) An object mapping logical phase names to their actual filenames in the `01_AI-RUN` directory.

## 2. Filename Mapping

To ensure the AI agent uses the correct filenames for each workflow phase, a `filenameMapping` object can be included in [`project_session_state.json`](project_session_state.json:1). This mapping should be manually updated if the filenames in `01_AI-RUN` are changed.

Example `filenameMapping`:

```json
{
  "gettingStarted": "01_Getting_Started.md",
  "autoPilot": "02_AutoPilot.md",
  "ideaGeneration": "03_Idea.md",
  "marketResearch": "04_Market_Research.md",
  "coreConcept": "05_Core_Concept.md",
  "prdGeneration": "06_PRD_Generation.md",
  "specsDocs": "07_Specs_Docs.md",
  "taskManager": "09_Task_Manager.md",
  "implementation": "08_Start_Building.md",
  "testing": "10_Testing.md",
  "deployment": "11_Deployment.md"
}
```

The AI agent should prioritize using the filenames from this mapping if it exists, falling back to the logical names if the mapping is not present or a specific logical name is not found in the mapping.