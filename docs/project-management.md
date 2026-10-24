# 10. Project Management and Risks

## 10.1 Repository

The project uses one GitHub repository: https://github.com/NurkhuzhayevaShinaray/fraud-risk-assessment. It is organised as src/ (backend, ml, frontend), docs/, diagrams/, tests/ and config/. Work is done in task branches named after the YouTrack task (for example ALQ-23-Complete-Literature-Review) and merged through pull requests that another team member reviews, and every commit message carries the task ID. The tags pre-defense-1, pre-defense-2 and final-pre-defense mark the submitted versions. No passwords, keys or personal data are committed.

## 10.2 YouTrack

The YouTrack project Alay-Aq (key ALQ) contains 19 planned work items covering the proposal, research, system comparison, technical decisions, requirements, architecture, UX design, evaluation planning and pre-defense preparation. Each task has one assignee, a priority, a deadline and acceptance criteria, and contributions from other students are recorded in the task description, comments, commits or pull requests.

## 10.3 Responsibilities

| Team member | Role | Main responsibilities |
|---|---|---|
| Kissami Shakhnaz | ML/NLP and Speech Analysis | Datasets; text classification; speech-to-text; risk assessment method; ML evaluation; ML service and its contract |
| Nurkhuzhayeva Shinaray | Backend and System Architecture | REST API, database, ML integration, architecture and diagrams, technology comparison, requirements specification, backend testing, API documentation, and GitHub repository management. |
| Botabaeva Saltanat | Frontend, Analytics, QA and Documentation | Five application pages and Figma mockups, user research and evidence of relevance, usability testing, quality assurance, project documentation, YouTrack project setup, task assignment, and progress tracking. |
| Serek Azamat Galymzhanovich | Supervisor | Feedback on key deliverables and decisions; review of significant changes at agreed checkpoints |

## 10.4 Milestones

Dates after the first pre-defense will be agreed with the supervisor.

| # | Milestone | Content | Date |
|---|---|---|---|
| M1 | First pre-defense | Proposal, evidence of relevance, literature review, system and technology comparisons, requirements, diagrams, UX prototype, verification plan, repository and YouTrack | 24 October 2026 |
| M2 | Backend prototype with mocked ML | Working REST API, database schema with content, validation, error handling, first automated tests | To be agreed |
| M3 | ML integration | Real ML service connected through the agreed contract; text and audio flows work end to end | To be agreed |
| M4 | Full application | Frontend connected to all endpoints; Learn, Safety Assistant and news working | To be agreed |
| M5 | Testing and evaluation | Documented test cases executed; ML evaluation; usability test; fixes | To be agreed |
| M6 | Final pre-defense | Documentation, limitations, demonstration of the complete system | To be agreed |

## 10.5 Risks

| ID | Risk | Likelihood | Impact | Mitigation | Owner |
|---|---|---|---|---|---|
| R1 | Reliable processing is not available for Kazakh or Russian text and audio | High | High | Language feasibility check early; document supported languages; do not present unsupported languages as completed | ML |
| R2 | Speech-to-text quality is too low for useful analysis | Medium | High | Compare existing models on sample recordings; restrict formats and duration; report word error rate | ML |
| R3 | The ML service is late or its interface changes | Medium | High | Agree the JSON contract now; develop against a mock service; version the contract | Backend and ML |
| R4 | Audio processing takes too long for a normal request | Medium | Medium | Timeouts and clear errors; asynchronous job endpoint (GET /api/analyze/jobs/:id) if needed | Backend |
| R5 | Lack of suitable labelled data | Medium | High | Use public datasets; document dataset limitations; evaluate only where labelled data exist | ML |
| R6 | Uploaded recordings or messages expose personal data | Low | High | Temporary storage with deletion; no sensitive content in logs or database; synthetic test data only | Backend |
| R7 | News sources are unreliable or restrict automated use | Medium | Low | Use a small number of verified sources; allow manual news entries; treat automatic collection as optional | Backend |
| R8 | Scope grows beyond the available time | Medium | Medium | Keep the exclusions in the proposal; prioritise Must requirements; review scope at each milestone | All |
| R9 | Work is concentrated at the end and contributions are not traceable | Medium | Medium | YouTrack tasks with owners; small commits with task IDs; pull request reviews | All |

## 10.6 Dependencies

| Dependency | Description |
|---|---|
| Backend on ML | The text and audio endpoints need the ML service or its mock; the contract in Section 7.6 must be agreed first |
| Frontend on backend | The pages need the API contract and example responses; the backend provides a mock-friendly contract and sample data |
| ML on data | Model selection and evaluation depend on the datasets and their licences |
| Everyone on requirements | The requirements in Section 6 define the acceptance criteria for all components |
| Delivery on environment | A shared Docker Compose set-up is needed to run and test the full system |
