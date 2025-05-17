## 4. Non-Functional Requirements (NFRs) (AI to Propose Defaults, User to Adjust)
*AI Instruction: Propose sensible default NFRs. The user can then adjust these.*

### 4.1. Performance
*AI Proposal:*
*   Web Vitals (LCP, FID, CLS) should be in the 'Good' range.
*   Server-side (e.g., Supabase Edge Function if used) responses for typical API calls should be < 500ms under normal load.
*   Page transitions should feel instant.
`[User to Adjust/Confirm AI's Proposed Performance NFRs]`

### 4.2. Scalability
*AI Proposal:*
*   If Supabase is chosen, the system should leverage its inherent scalability for database and authentication.
*   Edge functions should be written statelessly to allow for easy scaling.
*   Target: Handle 1000 concurrent users with acceptable performance (as defined in 4.1) after initial launch phase.
`[User to Adjust/Confirm AI's Proposed Scalability NFRs]`

### 4.3. Security
*AI Proposal:*
*   All data transmission encrypted via HTTPS.
*   If Supabase is chosen, Row Level Security (RLS) policies should be implemented for all relevant tables.
*   Secure password handling (e.g., leveraging Supabase Auth if chosen, or a similar robust authentication service).
*   Protection against OWASP Top 10 vulnerabilities in any custom code (e.g., API routes in the chosen frontend framework, serverless functions in the chosen backend).
*   Regular dependency updates.
`[User to Adjust/Confirm AI's Proposed Security NFRs]`

### 4.4. Reliability and Availability
*AI Proposal:*
*   Target 99.9% uptime (leveraging the chosen hosting provider, e.g., Vercel, and backend infrastructure, e.g., Supabase).
*   Implement robust error handling and logging in serverless functions/backend and frontend.
*   Utilize automated backups provided by the chosen database service (e.g., Supabase).
`[User to Adjust/Confirm AI's Proposed Reliability/Availability NFRs]`

### 4.5. Maintainability
*AI Proposal:*
*   Code will adhere to styles defined in Section 9.2.
*   AI will generate code documentation as per Section 9.4.
*   Modular design (Atomic Design for frontend, well-defined Edge Functions).
`[User to Adjust/Confirm AI's Proposed Maintainability NFRs]`

### 4.6. Usability and Accessibility (UX/UI & A11Y)
*AI Proposal:*
*   **Superior UX/UI Objective:** The application must offer an exceptionally intuitive, fluid, and aesthetically refined user experience, aiming for the standards of top "Silicon Valley / Y Combinator" applications.
*   Adherence to Agentic Design Principles (Section 5.1) which must embody this objective.
*   WCAG 2.1 AA compliance as a minimum target, with particular attention to an accessible and enjoyable user experience for all.
*   Semantic HTML, keyboard navigability, sufficient color contrast, and attention to interaction details.
`[User to Adjust/Confirm AI's Proposed Usability/Accessibility NFRs]`

### 4.7. Compatibility (Browsers, Devices, OS)
*AI Proposal:*
*   Latest two versions of major browsers: Chrome, Firefox, Safari, Edge.
*   Responsive design for desktop, tablet, and mobile.
*   Primary OS: Web-based, so OS agnostic.
`[User to Adjust/Confirm AI's Proposed Compatibility NFRs]`

### 4.8. Regulatory Compliance (AI to Query User if Potentially Relevant)
*AI Instruction: Based on the project idea (e.g., if it involves PII, health data, financial data), ask the user if specific regulations like GDPR, HIPAA, CCPA, etc., apply. If yes, note them here and ensure security/data handling plans reflect this.*
`[AI to Query User or state "No specific regulations identified by user at this stage."]`

### 4.9. Documentation (Product & Technical)
*AI Proposal:*
*   This PRD serves as the core product documentation.
*   AI will generate code-level documentation (JSDoc, comments).
*   AI will generate Storybook stories for UI components.
*   AI will generate basic API documentation if custom APIs are built.
`[User to Adjust/Confirm AI's Proposed Documentation Plan]`

### 4.10. NFR Verification Criteria for AI Agent
*AI Instruction: For each NFR above, you will define specific, verifiable criteria in your detailed feature specifications (Section 9.1) that your generated code must meet. E.g., for Performance: "Ensure all database queries generated for the chosen database (e.g., Supabase) use appropriate security mechanisms (like RLS) and table indexes where applicable."*
`[This section is a directive to the AI for its internal processes]`

--- 