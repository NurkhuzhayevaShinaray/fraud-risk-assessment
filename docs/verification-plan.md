# 9. Verification and Evaluation Plan

## 9.1 Scope

This section describes the backend and integration tests in detail. The evaluation of the ML models is shared with the ML contributor, and the final model, languages, datasets and experimental setup are confirmed by Kissami Shakhnaz.

## 9.2 Test Levels

| Level | What is tested | Tools (planned) | Owner |
|---|---|---|---|
| Unit tests | Validation rules, services, error mapping | Jest or Vitest | Backend |
| API / integration tests | Endpoints with a real database and a mocked ML service | Supertest, Docker Compose | Backend |
| ML integration tests | The backend with the real ML service, using the agreed contract | Scripted requests | Backend and ML |
| File handling tests | Accepted and rejected formats, size limits, corrupted files, cleanup of temporary files | Scripted requests, file system checks | Backend |
| Error handling tests | ML timeout, ML unavailable, malformed ML response, database error | Mock service, stopped containers | Backend |
| Usability tests | Main scenarios on the five pages | Task-based test with users | Frontend and QA |
| Performance check | Response time of the text and audio endpoints | Repeated scripted requests | Backend |

## 9.3 Test Cases (backend and integration)

The team must document at least 20 test cases in total. The backend part below has 24 cases; frontend and usability cases are added by Botabaeva Saltanat.

| ID | Scenario | Input | Expected result | Requirement |
|---|---|---|---|---|
| TC-01 | Valid text | Typical suspicious message | 200, risk level, indicators, explanation, recommendations | FR-01, FR-03 to FR-06 |
| TC-02 | Empty text | Empty string | 400 VALIDATION_ERROR | FR-02 |
| TC-03 | Text over the length limit | Text longer than the limit | 400 VALIDATION_ERROR | FR-02 |
| TC-04 | Missing text field | Body without text | 400 VALIDATION_ERROR | FR-02 |
| TC-05 | Unsupported language | Unsupported language value | Clear error or documented fallback | FR-07 |
| TC-06 | Valid audio | Supported file within limits | 200 with assessment; transcript when FR-11 is implemented | FR-08, FR-10, FR-11 |
| TC-07 | Unsupported format | A text or image file sent as audio | 415 UNSUPPORTED_MEDIA_TYPE | FR-09 |
| TC-08 | Renamed non-audio file | Text file named .mp3 | Rejected | NFR-03 |
| TC-09 | File over the size limit | Large file | 413 FILE_TOO_LARGE | FR-09 |
| TC-10 | Corrupted audio | Truncated file | 422 UNPROCESSABLE_AUDIO | FR-12 |
| TC-11 | Silent audio | Recording without speech | 422 UNPROCESSABLE_AUDIO with a clear message; no fraud-risk result | FR-12 |
| TC-12 | Temporary file cleanup after success | Valid audio | No file remains after the response | FR-25 |
| TC-13 | Temporary file cleanup after failure | Audio that causes an ML error | No file remains after the response | FR-25 |
| TC-14 | ML service unavailable | ML service stopped | 503 ML_UNAVAILABLE, backend keeps running | FR-16, NFR-07 |
| TC-15 | ML timeout | Mock service that answers too slowly | 504 ML_TIMEOUT | FR-15 |
| TC-16 | Malformed ML response | Mock service returns invalid JSON structure | 502 ML_BAD_RESPONSE | FR-17 |
| TC-17 | Learn list | GET /api/learn | 200, list of materials | FR-18 |
| TC-18 | Learn detail, existing ID | GET /api/learn/:id | 200, full content | FR-19 |
| TC-19 | Learn detail, unknown ID | Unknown ID | 404 NOT_FOUND | FR-19 |
| TC-20 | Safety Assistant, valid scenario | Existing scenario code | 200, ordered guidance steps | FR-20 |
| TC-21 | Safety Assistant, unknown scenario | Unknown code | 400 VALIDATION_ERROR | FR-20 |
| TC-22 | Error format consistency | Trigger 400, 404, 503 | All use the same error structure | FR-28 |
| TC-23 | No sensitive content in logs and database | Submit a known test text and audio | The text and audio do not appear in logs or tables | FR-29, NFR-04 |
| TC-24 | Health check | GET /api/health with and without the ML service | Status reflects each component | FR-30 |

## 9.4 Outcome Metrics and Measurement Conditions

| Aspect | Metric | How and under what conditions it is measured |
|---|---|---|
| Functional correctness | Share of test cases passed; all Must requirements covered by at least one passing test | Full test suite run with one command on the demonstration environment |
| Responsiveness | 95th percentile response time for text and audio endpoints | A fixed number of repeated requests with typical inputs on one reference machine, warm service, mocked and real ML service reported separately |
| Reliability | Backend stays available during simulated ML, database and file failures | Failure injection in TC-14 to TC-16 |
| Privacy | No original text or audio retained | Inspection of logs, tables and file storage after test runs (TC-12, TC-13, TC-23) |
| Classification quality (joint with ML) | Precision, Recall, F1-score, ROC-AUC, confusion matrix, false positives and false negatives | On a held-out labelled test set, reported per language |
| Transcription quality (joint with ML) | Word error rate | On a small set of recordings with reference transcripts |
| Usability | Task completion rate and user comments | Task-based test with at least five users |

## 9.5 Baseline Solutions for Comparison

| Component | Baseline | Compared with |
|---|---|---|
| Text risk assessment | A rule-based baseline using keyword and pattern indicators | The selected ML method |
| Text risk assessment | A classical model such as TF-IDF with Logistic Regression | The selected ML method, if a more complex method is used |
| Backend responsiveness | Response time of the mocked ML service (the overhead of the backend alone) | Response time with the real ML service |

The rule-based baseline is supported by the literature review, which describes rule-based detection as a baseline or supplementary component. The final choice of ML baselines is confirmed with the ML contributor.

## 9.6 Test Environment and Release Criteria

The test environment is Docker Compose with the backend, PostgreSQL and the ML service (or the mock service). Test data consists only of synthetic and public examples, with no real users' messages or recordings, and is kept in the repository without personal data. The prototype is ready for release when all Must requirements are verified, all documented test cases are executed with failures recorded, and known limitations (languages, formats, accuracy) are documented.
