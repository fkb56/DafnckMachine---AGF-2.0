## 1. Introduction and Objectives

### 1.1. Document Purpose
*Comment: This document serves as the primary input for the AI Coding Agent, which will elaborate on technical specifications based on the user's high-level input. It outlines the project idea, desired features, and establishes the framework for the AI to propose detailed solutions within the "Agentic Coding System".*
`[AI to summarize after initial user input]`

### 1.2. Project Idea & Core Problem (User Input)
*User Instruction: Please provide the core idea of your project and the main problem it aims to solve. Be as clear and concise as possible. The AI Agent can elaborate further if market research data is available or if it's instructed to perform high-level research.*
`[User to provide Project Idea and Core Problem]`

### 1.3. Product Vision (AI to Propose, User to Validate)
*Comment: Based on the user's idea, the AI will propose a long-term vision for the product.*
*AI Instruction: Based on the `Project Idea & Core Problem`, propose a compelling product vision. Consider potential impact and future evolution.*
`[AI to Propose Product Vision for User Validation]`

### 1.4. Business Goals (AI to Propose based on Idea, User to Validate)
*Comment: The AI will propose SMART business goals aligned with the project idea.*
*AI Instruction: Based on the `Project Idea & Core Problem`, propose 2-3 SMART (Specific, Measurable, Achievable, Relevant, Time-bound) business goals.*
`[AI to Propose Business Goals for User Validation]`

### 1.5. Key Performance Indicators (KPIs) (AI to Propose, User to Validate)
*Comment: The AI will propose KPIs to measure the success of the proposed business goals.*
*AI Instruction: For each proposed Business Goal, suggest 1-2 relevant KPIs.*
`[AI to Propose KPIs for User Validation]`

### 1.6. Project Scope (AI to Propose based on Features, User to Validate)
*Comment: The AI will define the initial scope based on the user's feature list.*
*AI Instruction: Based on the `High-Level Feature List` (Section 3.1), define what is IN SCOPE for the initial development phase.*
`[AI to Propose Project Scope for User Validation]`

### 1.7. Out of Scope (AI to Propose, User to Validate)
*Comment: The AI will suggest items that are explicitly out of scope for clarity.*
*AI Instruction: Based on the `Project Scope`, identify and list key items that are OUT OF SCOPE for this initial phase.*
`[AI to Propose Out of Scope items for User Validation]`

### 1.8. Guiding Principles for the AI Agent
*Comment: These are foundational principles for the AI's operation.*
*   **Excellence in Design and UX/UI:** The goal is to produce interfaces and user experiences of exceptional quality, worthy of the highest standards (like "Silicon Valley / Y Combinator"). This takes precedence over mere functionality.
*   Strict adherence to the Agentic Design System (Section 5.1 & 5.2), which must reflect this ambition.
*   Prioritize code clarity, maintainability, and testability.
*   Implement security best practices by default.
*   Optimize for performance as per NFRs (Section 4.1).
*   Generate comprehensive tests (unit, integration, assist with E2E).
*   Proactively propose solutions, libraries, MCP servers, and Supabase services, documenting rationale for human review.
*   Communicate ambiguities or need for clarification promptly (Section 9.1.10).
*   Follow all instructions within this PRD meticulously.
*   **Embrace Iterative Exploration:** Be prepared to generate multiple alternatives for UI components, logic flows, or technical solutions when prompted or when a clear optimal path isn't immediately evident from the PRD. The goal is to rapidly explore the solution space with human guidance, facilitating quick feedback and 'vibe-driven' development. Clearly label exploratory suggestions versus production-ready proposals.
*   **Contextual Awareness:** Strive to understand the broader project context by referring to all relevant sections of this PRD, existing codebase (if available and accessible as per Section 1.10.1), and project documentation before making decisions or generating code.
`[User can add specific overriding principles if any]`

### 1.9. Agentic Coding System Overview
*Comment: This system emphasizes technical excellence, design finesse, close Design <> Dev collaboration (even with AI), exhaustive documentation, and rapid iteration.*
*   **Core Tenets:**
    *   **Technical Excellence:** Clean, well-tested, performant, and maintainable code.
    *   **Design Finesse:** Meticulous attention to detail, resulting in a polished and intuitive user experience. Adherence to the `[AI to Propose Project Name] Design System` is paramount.
    *   **Collaboration:** Seamless integration between user requirements and AI execution, facilitated by this PRD and AI's clarification process.
    *   **Documentation:** AI-assisted generation of comprehensive documentation for code, design system components, and APIs.
    *   **Iteration:** AI facilitates rapid development cycles based on feedback and continuous improvement.
`[AI to ensure its processes align with these tenets]`

### 1.10. Default Technology Stack & AI Initiative in Tooling
*Comment: Defines the default technical foundation and AI's role in tool selection.*
This project suggests the following default technology stack, which can be overridden by user input in Section 5.4:
*   **Suggested Frontend:** Next.js (with TypeScript)
*   **Suggested Backend/Database:** Supabase (PostgreSQL, Auth, Storage, Edge Functions)
*   **Suggested Styling:** Tailwind CSS (with a custom Design System inspired by Shadcn/ui, as per Section 5.2)
The final choice of technologies will be determined by the user, considering project requirements and analyses.

The AI Coding Agent is empowered and expected to:
1.  Select appropriate, stable versions for the core stack elements.
2.  Identify, research, propose, and integrate relevant auxiliary libraries, **MCP servers** (e.g., for payments via Stripe MCP, advanced search, specific data processing via custom MCPs, documentation lookups via Context7 MCP, direct Supabase interactions via Supabase MCP, GitHub operations via GitHub MCP), and third-party APIs compatible with the chosen stack to best achieve the project goals. Task management is handled by Roo Orchestrator/Code (see [`../../../02_AI-DOCS/TaskManagement/Roo_Task_Workflow.md`](../../../02_AI-DOCS/TaskManagement/Roo_Task_Workflow.md)).
3.  If Supabase is chosen, leverage its features (Auth, Storage, Realtime, Edge Functions, Vector DB for AI features, etc.) extensively as the backend solution.
4.  All such selections and proposed integrations will be documented by the AI in its detailed feature specifications (as per Section 9.1) or in a dedicated 'Proposed Technical Solutions & Integrations' section for human review and approval before implementation.

#### 1.10.1. Access to Project Context for AI Agent
*AI Agent Directive: For optimal understanding and consistency, you will have access to (or must request access to, if not immediately available) the following project context elements:*
*   *The complete Git repository of the project (once initiated).*
*   *Key configuration files (e.g., `tailwind.config.js`, `tsconfig.json`, `package.json`, framework-specific configuration like `next.config.js` if Next.js is chosen, Vercel/chosen hosting provider and Supabase/chosen backend environment variables).*
*   *Existing Storybook documentation (if any).*
*   *Database schemas (e.g., Supabase Studio interface or migration files if Supabase is chosen).*
*   *Documentation for known/integrated MCPs (via Context7 MCP or provided links).*
*   *When performing tasks like feature decomposition (Section 9.1) or code generation, actively refer to this context to ensure coherence and accuracy.*
`[User can note any immediate exclusions or preferences here]`

### 1.11. AI-Human Interaction and Validation Protocol
*Comment: This section defines how the AI Agent and human stakeholders will interact for proposals, validations, and conflict resolution. The AI Agent must maintain an internal state of tasks (TODO, PENDING_SPEC_VALIDATION, READY_FOR_IMPLEMENTATION, IN_PROGRESS, PENDING_CODE_REVIEW/TESTING, DONE) and communicate this status clearly, potentially by interacting with Roo Orchestrator or by updating a status field in this PRD/linked document.*
*   **Proposal Mechanism:** The AI Agent will primarily update relevant sections of THIS PRD with its detailed proposals (e.g., proposed KPIs in 1.5, detailed feature specs in a separate linked document or appendix referenced from 9.1, proposed Design System tokens in 5.2). For significant proposals (new MCPs, major architectural choices, complex UI designs), the AI will explicitly state: 'PROPOSAL FOR VALIDATION: [details of proposal]' and list specific questions if any.
*   **Validation Channel:** The user will review these sections/proposals and provide feedback directly within the project's communication channel (e.g., comments in a shared document, dedicated Slack channel, or project management tool). Feedback should be clear (e.g., 'Approved', 'Approved with changes: [details]', 'Rejected, please reconsider [alternative/reason]').
*   **Conflict Resolution & Iteration:** If a human stakeholder disagrees with an AI proposal, the AI will be provided with the reasons or alternative suggestions. The AI must then revise its proposal, incorporating the feedback, and present a new option. This iterative feedback loop will continue until consensus is reached or the human stakeholder provides a definitive directive. The AI should log its previous proposals and the received feedback to learn and avoid repeating rejected suggestions.
*   **PRD Versioning:** After each significant cycle of AI proposals and human validation that leads to changes in the PRD, the AI Agent will increment the minor version of this PRD (e.g., from 1.0 to 1.1) and update the 'Last Updated' date.
*   **Waiting for Validation:** AI Agent, after submitting a proposal for validation, you must place that specific task in a 'PENDING_VALIDATION' state and await explicit human feedback before proceeding with implementation related to that proposal.

--- 