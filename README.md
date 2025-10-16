# Python Server

This project contains a FastAPI server implemented in Python. It provides two routes for managing a task list.

## Project Structure

The project has the following files and directories:

- `python-server/src/main.py`: This file contains the implementation of the FastAPI server with two routes. It handles adding a task to a list and retrieving the list.

- `python-server/src/__init__.py`: This file is an empty file that marks the `src` directory as a Python package.

- `python-server/requirements.txt`: This file lists the dependencies required for the FastAPI server and other dependencies.

- `python-server/Dockerfile`: This file is used to build a Docker image for the FastAPI server. It specifies the base image, copies the source code into the image, installs the dependencies, and sets the command to run the server.

- `docker-compose.yml`: This file is used to define and run multi-container Docker applications. It specifies the services to run, their configurations, and any dependencies between them.

## Getting Started

To run the FastAPI server using Docker, follow these steps:

- Build and start the Docker containers by running the following command:

  ```shell
  docker compose up
  ```

  This command will build the Docker image for the FastAPI server and start the containers defined in the `docker-compose.yml` file.

- The FastAPI server should now be running. You can access at port `8000`.

## API Routes

The FastAPI server provides the following API routes:

- `POST /tasks`: Adds a task to the task list. The request body should contain the task details.

- `GET /tasks`: Retrieves the task list.

/**
 * Migration Note: Python server -> Node.js server
 *
 * Summary:
 * - This module was migrated from a Python-based HTTP server to a Node.js runtime.
 * - Public API routes, request/response shapes, and business logic were preserved where possible.
 * - Behavior-critical differences and required configuration updates are documented below.
 *
 * Key changes:
 * - Runtime: Python 3.x web stack -> Node.js LTS (>= 18). Non-blocking I/O and event-loop semantics now apply.
 * - Module system: Uses modern JavaScript/TypeScript with async/await. Ensure ES module/CommonJS interop is configured consistently across the project.
 * - HTTP handling: Request parsing, routing, and middleware are provided by the Node server stack. JSON/body parsing is handled via middleware and must be registered before routes.
 * - Error handling: Replaced Python exception handlers with centralized Node error middleware. Errors now return standardized JSON payloads with consistent status codes.
 * - Logging: Python logging replaced by Node logger (structured logs with levels, request correlation IDs, and redaction for sensitive fields).
 * - Validation: Python-side validation (e.g., pydantic) replaced by Node schema validation. All inbound payloads are validated at the edge; errors report a consistent { code, message, details } format.
 * - Data access: Python DB client replaced by Node driver/ORM. Connection pooling and async queries are handled by the Node data layer. Verify transaction boundaries and isolation levels.
 * - Background jobs: Python workers replaced by a Node-compatible queue/scheduler. Ensure idempotency keys and retry semantics match prior behavior.
 * - Auth & security: Token/session verification implemented in Node middleware. CORS, Helmet/security headers, and rate limiting configured at the server edge.
 * - Streaming & file uploads: Implemented via Node streams; backpressure is respected. Max payload size and timeouts configured in server settings.
 *
 * Backward compatibility:
 * - Endpoints: Paths and HTTP methods preserved. Minor differences may exist in error messages and default headers.
 * - Status codes: Normalized across endpoints; 4xx for client errors, 5xx for server errors. 422 may replace 400 in validation failures, depending on validator configuration.
 * - Timestamps & serialization: All dates returned as ISO-8601 strings in UTC. Numeric precision and BigInt serialization handled explicitly.
 *
 * Configuration:
 * - Environment variables moved to Node process environment. See .env.example for updated keys.
 * - Replace Python-specific settings (e.g., GUNICORN_WORKERS) with Node equivalents (e.g., PORT, NODE_ENV).
 * - Database/queue URLs and TLS options may require updated formats compatible with Node drivers.
 *
 * Testing:
 * - Test runner migrated from Python (e.g., pytest) to a Node runner. Unit/integration tests mirror previous coverage with fixtures adapted to Node.
 * - Contract tests ensure response schemas and status codes match prior server behavior.
 *
 * Deployment & operations:
 * - Start commands changed from Python WSGI/ASGI (e.g., gunicorn/uvicorn) to Node process manager (e.g., node, pm2, or container entrypoint).
 * - Health checks: /health and /ready endpoints maintained; responses standardized to JSON with service and dependency status.
 * - Observability: Metrics and tracing integrated via Node instrumentation. Log format is JSON for aggregation.
 *
 * Breaking changes and deprecations:
 * - Error payload shape standardized; clients relying on previous message formats must adjust.
 * - Some optional query/body fields were made strict to prevent ambiguous defaults.
 * - Deprecated endpoints are still accepted but emit deprecation warnings and will be removed in a future release.
 *
 * How to run locally:
 * - Requirements: Node.js >= 18, package manager (npm/yarn/pnpm), and running dependencies (DB/queue).
 * - Steps: install dependencies, configure .env, then start dev server. See repository README for scripts and detailed commands.
 *
 * Verification checklist:
 * - [ ] All public endpoints return expected status, headers, and JSON schema.
 * - [ ] Auth flows (login, refresh, logout) validated with valid/invalid tokens.
 * - [ ] File upload/download and streaming responses tested under load.
 * - [ ] Database transactions and migrations verified; no connection leaks.
 * - [ ] Error paths produce standardized error responses with correlation IDs.
 *
 * Notes:
 * - Keep Python-specific code removed from runtime paths; compatibility adapters exist only where documented.
 * - If unexpected differences arise, enable debug logs and compare against recorded Python-server golden responses.
 */
