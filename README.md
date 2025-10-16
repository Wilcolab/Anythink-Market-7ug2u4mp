# Anythink Market - Multi-Server Setup

This project contains both a FastAPI server implemented in Python and an Express.js server implemented in Node.js. Both servers provide identical API routes for managing a task list and run simultaneously.

## Project Structure

The project has the following files and directories:

### Python Server
- `python-server/src/main.py`: This file contains the implementation of the FastAPI server with API routes for task management.
- `python-server/src/__init__.py`: This file is an empty file that marks the `src` directory as a Python package.
- `python-server/requirements.txt`: This file lists the dependencies required for the FastAPI server.
- `python-server/Dockerfile`: This file is used to build a Docker image for the FastAPI server.

### Node.js Server
- `node-server/express-server-project/src/server.js`: This file contains the implementation of the Express.js server with matching API routes.
- `node-server/express-server-project/src/routes/index.js`: This file contains route definitions for the Express server.
- `node-server/express-server-project/package.json`: This file lists the dependencies and scripts for the Node.js server.
- `node-server/express-server-project/Dockerfile`: This file is used to build a Docker image for the Express server.
- `node-server/express-server-project/nodemon.json`: Configuration file for nodemon development server.

### Shared Configuration
- `docker-compose.yml`: This file defines and runs multi-container Docker applications for both servers.
- `README.md`: This documentation file.

## Getting Started

To run both servers using Docker, follow these steps:

1. **Build and start the Docker containers** by running the following command:

   ```shell
   docker compose up --build
   ```

   This command will build Docker images for both the FastAPI and Express servers and start the containers.

2. **Access the servers**:
   - **Python FastAPI server**: Running on `http://localhost:8000`
   - **Node.js Express server**: Running on `http://localhost:8001`

Both servers support hot-reloading for development:
- Python server uses `uvicorn` with `--reload`
- Node.js server uses `nodemon` for automatic restarts on code changes

## API Routes

Both servers provide identical API routes:

### Root Endpoint
- `GET /`: Returns a simple "Hello World" message

### Task Management
- `GET /tasks`: Retrieves the current task list
  - **Response**: `{"tasks": ["task1", "task2", ...]}`
- `POST /tasks`: Adds a new task to the list
  - **Request Body**: `{"text": "Your task description"}`
  - **Response**: `{"message": "Task added successfully"}`
  - **Error Response**: `{"message": "Task text is required"}` (400 status)

### Example Usage

```bash
# Get tasks from Python server
curl http://localhost:8000/tasks

# Get tasks from Node.js server
curl http://localhost:8001/tasks

# Add a task to Python server
curl -X POST http://localhost:8000/tasks \
  -H "Content-Type: application/json" \
  -d '{"text": "New task"}'

# Add a task to Node.js server
curl -X POST http://localhost:8001/tasks \
  -H "Content-Type: application/json" \
  -d '{"text": "New task"}'
```

## Development

Both servers maintain the same in-memory task list independently. Changes to one server do not affect the other.

### Adding New Features
When adding new endpoints or features:
1. Implement in both `python-server/src/main.py` and `node-server/express-server-project/src/server.js`
2. Ensure API contracts remain identical
3. Test both servers independently
4. Update this README with new routes

### Migration Notes
The Node.js server was created to mirror the Python FastAPI implementation, ensuring feature parity and identical API behavior.
