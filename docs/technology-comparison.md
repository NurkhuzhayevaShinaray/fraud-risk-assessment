# 5. Technology Comparison

## 5.1 Purpose and Method

This section compares alternatives for four technical decisions in the backend and system architecture. Each decision is compared on the same criteria against the requirements in Section 6, and the choice is justified in a short paragraph. Statements about the technologies are based on their official documentation (see 5.6).

## 5.2 Decision 1: Backend Platform

Which platform runs the REST API, validates requests, handles file uploads and coordinates the database and the ML module? The alternatives are Node.js with Express.js written in TypeScript (A1), Python with FastAPI (A2), and Python with Django and Django REST Framework (A3).

| Criterion | A1. Express + TypeScript | A2. FastAPI | A3. Django + DRF |
|---|---|---|---|
| Fit with the frontend | Same language family as the JavaScript frontend; the team can read the API code | Different language from the frontend | Different language from the frontend |
| Integration with the Python ML module | Requires a separate service or bridge | Can call ML code directly or through a service | Can call ML code directly or through a service |
| File upload | Available through middleware libraries such as multer | Built-in upload handling | Built-in file handling |
| Input validation | Needs a validation library (for example Zod) | Built-in validation from type hints (Pydantic) | Serializers in DRF |
| API documentation | Added with OpenAPI/Swagger tooling | Generated automatically (OpenAPI) | Added with extra packages |
| Structure and amount of boilerplate | Minimal and flexible; structure is chosen by the team | Light and modern | Heavier; many built-in features (ORM, admin, authentication) |
| Type safety | Provided by TypeScript, which makes the API contract explicit | Provided by Python type hints | Limited by default |
| Team learning effort | Backend developer is learning TypeScript | Backend developer needs to be comfortable with Python | Larger framework to learn |

Decision: A1, Node.js with Express.js in TypeScript. The frontend is written in JavaScript, so one language family covers the web layers and the team can read each other's code. Express is minimal, which suits a prototype with a few endpoints, and TypeScript lets the request and response shapes be written as types that match the API contract in Section 7.6. FastAPI is a strong alternative, especially for ML integration, but it would put the backend in a different language from the frontend, and Django brings an admin panel and built-in authentication that the project does not use. The main cost is that Node.js cannot call the Python ML module directly, which is handled in 5.4. If TypeScript slows development, the code can stay plain JavaScript without changing the architecture.

## 5.3 Decision 2: Database

Where is persistent application data stored? The alternatives are PostgreSQL (B1), MongoDB (B2) and SQLite (B3).

| Criterion | B1. PostgreSQL | B2. MongoDB | B3. SQLite |
|---|---|---|---|
| Data model | Relational tables with defined relations; JSON column support for flexible fields | Document collections with a flexible schema | Relational tables in a single local file |
| Fit with project data | Educational content, fraud types, recommendations, indicators and assessment records have clear relations | Possible, but the data is not naturally document-shaped | Fits the data structure |
| Querying and filtering | Full SQL, joins, aggregations | Query language and aggregation pipeline | SQL, with fewer advanced features |
| Data integrity | Transactions and constraints | Document-level atomicity; multi-document transactions are supported in some configurations | Transactions and constraints |
| Concurrent access and deployment | Separate database server; runs well in Docker | Separate database server | No server, but limited support for concurrent writes |
| Support in Node.js and TypeScript | Mature libraries and ORMs such as Prisma and node-postgres | Mature libraries | Supported through libraries |
| Setup effort | Moderate; simplified by Docker | Moderate | Very low |

Decision: B1, PostgreSQL. The data is structured and related (a safety scenario has ordered steps, an assessment has several indicators), which fits a relational database, and PostgreSQL can also store flexible fields such as indicator lists as JSON. The flexible schema of MongoDB is not needed because the structure is known, and SQLite suits single-user or embedded use better than a multi-user web application. PostgreSQL needs a server and migrations, and Docker Compose with a migration tool such as Prisma keeps that effort small.

## 5.4 Decision 3: Communication Between the Backend and the ML Module

How does the Express backend send text or audio to the ML module and receive the results? The alternatives are a separate ML service called through HTTP (C1), a message queue with asynchronous jobs (C2), and running the Python code from Node.js as a child process or in-process call (C3).

| Criterion | C1. HTTP ML service | C2. Message queue | C3. Child process / in-process |
|---|---|---|---|
| Independence of components | High; the ML service is deployed and developed separately | High | Low; the backend depends directly on the ML code and runtime |
| Parallel work by the team | Easy once the JSON contract is agreed | Easy once the message contract is agreed | Harder; both parts share one runtime |
| Fit for long audio processing | Works for short jobs; long jobs need a job ID and polling | Designed for long-running asynchronous jobs | Blocks or needs extra process management |
| Implementation complexity | Low to moderate | Higher (additional infrastructure) | Low initially, but difficult to maintain |
| Error handling for an unavailable ML service | Timeouts, retries and clear HTTP error codes | Retries and dead-letter handling are built into many queue systems | Process crashes are harder to isolate |
| Testing | The backend can be tested with a mocked ML service | Requires a queue in the test environment | Harder to isolate |
| Deployment | Two containers | Three or more containers | One deployment, but with a mixed runtime |

Decision: C1, a separate ML service called over HTTP. The ML module is expected to be in Python and the backend is Node.js, so the two should be separate components joined by a JSON contract. The backend can then be built and tested against a mock ML service while the real one is in progress, and it can apply timeouts and map failures to clear API errors. A message queue suits long or high-volume jobs but adds infrastructure that a prototype does not need, and running Python from Node.js would couple the components and make failures hard to isolate. If long audio exceeds a normal request time, the API will return a job ID and the frontend will poll for the result, without changing the architecture. The ML service stays a single point of failure, so the backend returns a clear error when it is unavailable, and the contract must be versioned.

## 5.5 Decision 4: Handling Uploaded Audio Files

How are uploaded recordings stored and processed? The alternatives are temporary storage deleted after processing (D1), persistent storage on the server disk (D2), and persistent storage in external object storage (D3).

| Implementation complexity | Low | Low | Higher (account, configuration, cost) |
|---|---|---|---|
| Reprocessing and history | Not possible after deletion | Possible | Possible |
| Security responsibility | Limited to validation and safe cleanup | Access control and retention policy are needed | Access control and provider configuration are needed |

Decision: D1, temporary storage with deletion after processing. The aim is to keep as little sensitive user content as possible, and temporary storage meets it with the lowest complexity. The backend validates the file type and size, passes the file to the ML service and deletes it afterwards, including after errors, and only the analysis result is stored in the database. The cost is that a failed analysis cannot be re-run without a new upload, and cleanup must be tested on error paths.

## 5.6 References

1. Express.js documentation: https://expressjs.com
2. TypeScript documentation: https://www.typescriptlang.org/docs
3. FastAPI documentation: https://fastapi.tiangolo.com
4. Django documentation: https://docs.djangoproject.com
5. Django REST Framework documentation: https://www.django-rest-framework.org
6. PostgreSQL documentation: https://www.postgresql.org/docs
7. MongoDB documentation: https://www.mongodb.com/docs
8. SQLite documentation: https://www.sqlite.org/docs.html
9. Prisma documentation: https://www.prisma.io/docs
10. RabbitMQ documentation: https://www.rabbitmq.com/docs
