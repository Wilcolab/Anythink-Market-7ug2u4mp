# Express Server

This project contains an Express server implemented in JavaScript. It listens on port 8001 and is set up for automatic code reloading using Nodemon.

## Project Structure

The project has the following files and directories:

- `src/server.js`: This file is the entry point of the application. It creates an instance of the Express app and sets it to listen on port 8001.

- `src/routes/index.js`: This file is intended for defining routes but currently does not export any routes since there are no endpoints defined.

- `.dockerignore`: This file specifies which files and directories should be ignored when building the Docker image.

- `Dockerfile`: This file is used to build a Docker image for the Express server. It specifies the base image, copies the source code into the image, installs the dependencies, and sets the command to run the server.

- `nodemon.json`: This file contains configuration settings for Nodemon, specifying how it should monitor files and restart the server on changes.

- `package.json`: This file is the configuration file for npm. It lists the dependencies (including Express and Nodemon) and scripts for the project, including a start script that runs Nodemon.

## Getting Started

To run the Express server, follow these steps:

1. Install the dependencies by running the following command:

   ```shell
   yarn install
   ```

2. Start the server with Nodemon using the following command:

   ```shell
   yarn start
   ```

3. The Express server should now be running and listening on port `8001`.

## API Routes

Currently, there are no defined API routes in this project. You can add routes in the `src/routes/index.js` file as needed.