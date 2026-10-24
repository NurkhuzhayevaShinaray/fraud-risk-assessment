# 6. Requirements Specification

## 6.1 Purpose and Conventions

This section defines what the system must do (functional requirements) and the qualities it must have (non-functional requirements). Each requirement has a priority and an acceptance criterion, so that every mandatory requirement can be verified.

Priority follows the MoSCoW scheme: Must means the requirement is mandatory for the prototype, Should means it is planned but the prototype still works without it, and Could means it is desirable if time allows. In the verification column, T is a test, I is an inspection of code, configuration or documents, and D is a demonstration.

## 6.2 Functional Requirements

### 6.2.1 Text analysis

| ID | Requirement | Priority | Acceptance criterion | Verif. |
|---|---|---|---|---|
| FR-01 | The system shall accept text submitted by the user for fraud risk assessment. | Must | A valid text request to the text endpoint returns a successful response with an assessment. | T |
| FR-02 | The system shall validate text input (not empty, within the maximum length). | Must | An empty text or text over the maximum length returns a validation error with a clear message and no assessment. | T |
| FR-03 | The system shall return a risk level of Low, Medium or High. | Must | Every successful assessment contains exactly one of the three levels. | T |
| FR-04 | The system shall return the detected suspicious indicators (for example urgency or a request for sensitive information). | Must | The response contains an indicators list; for a prepared set of sample messages, the expected indicators are returned. | T |
| FR-05 | The system shall return a short explanation of the assessment. | Must | The response contains a non-empty explanation in the language of the interface. | T |
| FR-06 | The system shall return practical safety recommendations based on the result. | Must | The response contains at least one recommendation for Medium and High risk. | T |
| FR-07 | The system shall accept a language parameter or detect the language of the text. | Should | Requests in each language confirmed by the feasibility check are processed; an unsupported language returns a clear message. | T |

### 6.2.2 Audio analysis

| ID | Requirement | Priority | Acceptance criterion | Verif. |
|---|---|---|---|---|
| FR-08 | The system shall accept an uploaded audio recording. | Must | A valid file in a supported format (for example WAV or MP3) returns a successful response with an assessment. | T |
| FR-09 | The system shall validate the file type, size and duration. | Must | A file of an unsupported type, over the size limit or over the duration limit is rejected with a clear error before processing. | T |
| FR-10 | The system shall transcribe the audio and assess the transcript. | Must | For a prepared sample recording, the response contains a risk level, indicators and recommendations obtained from the transcript. | T/D |
| FR-11 | The system shall return the transcript to the user. | Should | The response contains the transcript text; the transcript is not stored after the response (see NFR-04). | T |
| FR-12 | The system shall handle corrupted or empty audio. | Must | A corrupted or silent file returns a clear error and does not cause a server failure. | T |
| FR-13 | The system shall support asynchronous processing of long recordings (job ID and status check). | Could | If a job takes longer than the request timeout, the client receives a job ID and can later retrieve the result. | T |

### 6.2.3 ML integration

| ID | Requirement | Priority | Acceptance criterion | Verif. |
|---|---|---|---|---|
| FR-14 | The backend shall send submissions to the ML service through the agreed interface and receive structured results. | Must | With the ML service running, text and audio requests return results that match the documented API contract. | T |
| FR-15 | The backend shall apply a timeout when calling the ML service. | Must | When the ML service does not respond within the timeout, the API returns a timeout error. | T |
| FR-16 | The backend shall return a clear error when the ML service is unavailable. | Must | With the ML service stopped, the API returns a service-unavailable error and remains running. | T |
| FR-17 | The backend shall validate and normalize the ML output before returning it to the frontend. | Must | A malformed ML response is rejected and reported as an error; valid responses follow the contract. | T |

### 6.2.4 Learn, Safety Assistant and Home

| ID | Requirement | Priority | Acceptance criterion | Verif. |
|---|---|---|---|---|
| FR-18 | The system shall provide a list of educational materials about fraud techniques. | Must | The list endpoint returns all stored materials with title and short description. | T |
| FR-19 | The system shall provide the details of a selected fraud technique (warning signs and prevention). | Must | The detail endpoint returns the full content for an existing ID and a not-found error for an unknown ID. | T |
| FR-20 | The Safety Assistant shall return guidance for a situation selected by the user (for example, shared confidential data or a suspicious transfer). | Must | For each predefined situation, the endpoint returns guidance steps; an unknown situation returns a validation error. | T |
| FR-21 | The Safety Assistant guidance shall refer users to official channels where appropriate. | Should | Guidance for high-impact situations contains at least one reference to an official channel. | I |
| FR-22 | The system shall provide news and alerts about fraud for the Home page. | Should | The news endpoint returns a list of items with title, source and date. | T |
| FR-23 | The system shall collect news from verified sources automatically. | Could | News from configured sources is stored without duplicates and shown on the Home page. | T/D |

### 6.2.5 Data and files

| ID | Requirement | Priority | Acceptance criterion | Verif. |
|---|---|---|---|---|
| FR-24 | Educational content, safety guidance and news shall be stored in the PostgreSQL database. | Must | After a restart, the content remains available; the database schema includes at least four core tables for educational content, safety scenarios, safety steps and news. | T/I |
| FR-25 | Uploaded audio files shall be deleted after processing, including after errors. | Must | After successful and failed requests, no uploaded file remains in the temporary storage. | T |
| FR-26 | The system may store a non-sensitive assessment record (risk level, indicators, timestamp) if history is included. | Could | A record contains no original message text or audio and can be retrieved by ID. | T/I |

### 6.2.6 API and system

| ID | Requirement | Priority | Acceptance criterion | Verif. |
|---|---|---|---|---|
| FR-27 | The system shall expose a documented REST API with JSON, and multipart/form-data for audio. | Must | At least eight endpoints are implemented and documented with request, response and error examples. | I/T |
| FR-28 | All errors shall use one consistent format with a status code and a message. | Must | Validation, not-found, timeout and server errors return the same structure. | T |
| FR-29 | The system shall log important events and errors without logging sensitive content. | Must | Logs show requests, errors and ML calls; a test submission's text and audio do not appear in the logs. | I/T |
| FR-30 | The system shall provide a health-check endpoint. | Should | The endpoint reports the status of the backend, the database and the ML service. | T |
| FR-31 | The frontend shall provide five pages (Home, Fraud Checker, Results and Recommendations, Learn, Safety Assistant) connected to the API. | Must | Each page loads real data through the API (owner: frontend). | D |
| FR-32 | Every result shall state that the assessment is indicative and does not guarantee that a communication is fraudulent or legitimate. | Must | The results page displays this statement, and every successful assessment response includes a non-empty disclaimer field. | I/D |

## 6.3 Non-Functional Requirements

| ID | Category | Requirement | Priority | Acceptance criterion | Verif. |
|---|---|---|---|---|---|
| NFR-01 | Performance | Text assessment shall respond within a reasonable time under normal prototype load. | Should | 90% of text requests of typical length respond within a couple of minutes in the demonstration environment. | T |
| NFR-02 | Performance | Audio assessment shall complete within a reasonable time for recordings of supported duration. | Should | Processing of a recording of the maximum duration completes within 5-10 min, or an asynchronous job is used (FR-13). | T |
| NFR-03 | Security | All input, including uploaded files, shall be validated on the server. | Must | Requests with invalid fields, wrong content types or renamed non-audio files are rejected. | T |
| NFR-04 | Privacy | The system shall not permanently store original user messages or audio recordings. | Must | After a request is completed, the database, logs and file storage contain no original text or audio. | I/T |
| NFR-05 | Security | Secrets (database credentials, keys) shall be kept outside the source code and the frontend. | Must | The repository contains only .env.example with placeholders; the application reads secrets from the environment. | I |
| NFR-06 | Security | The API should limit the rate of requests from one client. | Should | Exceeding the limit returns a "too many requests" error. | T |
| NFR-07 | Reliability | Failure of the ML service, the database or a single request shall not stop the backend. | Must | After simulated failures, the backend continues to serve other requests. | T |
| NFR-08 | Usability | Error messages shown to users shall be understandable and indicate what to correct. | Should | For the listed error cases, the frontend shows a plain-language message (usability test with at least three users). | T/D |
| NFR-09 | Explainability | Results shall show why a message was assessed as risky. | Must | Every Medium or High result lists at least one indicator and an explanation. | T |
| NFR-10 | Maintainability | The backend code shall be organized in layers (routes, services, data access) and documented. | Should | The repository structure and README describe the layers; code review confirms separation. | I |
| NFR-11 | Testability | The system shall have automated API tests; together the team shall document at least 20 test cases. | Must | The test suite runs with one command, and the test documentation lists at least 20 cases (functional, integration, usability). | T/I |
| NFR-12 | Portability | The system shall start in a documented way on another computer. | Should | Following the README, a team member starts the backend, database and ML service. | D |
| NFR-13 | Compatibility | The frontend shall work in current versions of common browsers. | Should | The main scenarios work in the latest Chrome and one other browser. | T |
| NFR-14 | Localization | The system shall support the languages confirmed by the language feasibility check. | Should | Each supported language passes the language test set; limitations for other languages are documented. | T/I |
| NFR-15 | Traceability | Work shall be traceable in Git and YouTrack. | Must | Each task has an owner, acceptance criteria and a deadline; commits reference the task ID. | I |
