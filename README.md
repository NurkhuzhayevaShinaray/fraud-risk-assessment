# Fraud Risk Assessment Based on Text and Speech Analysis

Web application that estimates the risk of fraud in text messages and in audio/video recordings (speech), and gives the user security recommendations.

## Problem statement
<!-- Student C: from Project Brief. Fraud schemes use messages, phone calls and social engineering; most tools analyse only one channel. -->

## Target users
<!-- Student C -->

## Expected outcomes
<!-- Web app with REST API, database, text and speech ML modules, risk score (Low / Medium / High), recommendations, analytics. -->

## Team
| Member | Role | Responsibility |
|---|---|---|
| Shahnaz Kissami | ML / NLP and speech | Fraud categories, datasets, text and speech models |
| Shinaray Nurkhuzhayeva | Backend | REST API (Node.js/Express), PostgreSQL, ML integration, tests, API docs |
| Saltanat Botabaeva | Frontend / research | Project brief, research evidence, UX (Figma), frontend |

**Supervisor:** Серек Азамат Галымжанович

## Scope and status
Current stage: Foundation (analysis, design, planning). No runnable application yet.

## Selected technologies
Preliminary: Node.js + Express, PostgreSQL, Docker. Alternatives are compared in `docs/technology-comparison.md`.

## Links
- YouTrack: <!-- add link -->
- Documentation: [`docs/`](docs/)
- Prototype (Figma): <!-- add link -->

## Setup, run and test
To be added when runnable code is available. Copy `config/.env.example` to `.env` and fill in values.

## Repository structure
```
src/backend    REST API, database, integration
src/ml         text and speech models
src/frontend   user interface
docs/          proposal, review, comparisons, requirements, architecture
diagrams/      editable sources and exports
tests/         automated tests
config/        configuration examples
```

## Workflow
One YouTrack task per work item. Branch `DIP-XX-short-name`, commit `DIP-XX: message`, merge only through a reviewed pull request.
