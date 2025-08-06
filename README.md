# Todo App

A simple todo application with Node.js backend and React frontend.

## What it does

This app lets you create, edit, and delete todo items. It has a web interface where you can manage your tasks.

## How it works

The app has 4 parts:
- Frontend: React app for the user interface
- Backend: Node.js server that handles data
- Database: MongoDB to store todos
- Nginx: Web server that connects everything

## Files in this project

```
backend/          - Server code (Node.js)
  server.js       - Main server file
  package.json    - Backend dependencies
  Dockerfile      - Backend container setup

frontend/         - Web interface (React)
  src/
    App.jsx       - Main React component
    main.jsx      - App entry point
    index.css     - Styles
  package.json    - Frontend dependencies
  vite.config.js  - Build tool config
  Dockerfile      - Frontend container setup

nginx/            - Web server config
  nginx.conf      - Main web server settings
  conf.d/
    default.conf  - Route configuration
  Dockerfile      - Nginx container setup

docker-compose.yml - Runs all parts together
package.json      - Project settings
bitbucket-pipelines.yml - Auto deployment setup
```

## How to run

You need Docker installed on your computer.

1. Open terminal in project folder
2. Run this command:
   ```
   docker compose up
   ```
3. Wait for it to start
4. Open your browser and go to: http://localhost

## How to use

- Type in the box to add a new todo
- Click the checkbox to mark todo as done
- Click delete to remove a todo
- Click edit to change todo text

## API endpoints

The backend server provides these URLs:
- GET /api/todos - Get all todos
- POST /api/todos - Add new todo
- PUT /api/todos/ID - Update a todo
- DELETE /api/todos/ID - Delete a todo
- GET /api/health - Check if server is working

## Technology used

- Node.js - Server
- React - Frontend
- MongoDB - Database
- Docker - Container system
- Nginx - Web server

## Development

To make changes:
1. Edit files in backend/ or frontend/
2. Run docker compose up again
3. Check http://localhost to see changes

## Deployment

The app can be deployed using the bitbucket-pipelines.yml file which automatically builds and runs the app on your server.

### How Bitbucket runs the app

When you push code to Bitbucket:
1. Bitbucket sees the bitbucket-pipelines.yml file
2. It runs on your own server (self-hosted runner)
3. The pipeline does these steps:
   - Stops any running containers
   - Builds new containers with your latest code
   - Starts all services (database, backend, frontend, nginx)
   - Checks if the app is working
   - Reports success or failure

### Setting up auto deployment

To make this work you need:
1. Install Bitbucket runner on your server
2. Connect your server to Bitbucket
3. Push code changes to trigger deployment
4. Your app updates automatically

The pipeline file is very simple and only runs essential commands to deploy your app.
