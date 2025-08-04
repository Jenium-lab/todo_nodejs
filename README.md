# Simple Todo App

A fast and simple full-stack todo application built with Node.js and React.

## Features

- ✅ Create new todos
- ✅ Mark todos as complete/incomplete
- ✅ Edit existing todos
- ✅ Delete todos
- ✅ View todo statistics
- ✅ Responsive design
- ✅ Real-time updates

## Tech Stack

### Backend
- **Node.js** - Runtime environment
- **Express.js** - Web framework
- **MongoDB** - Database with Mongoose ODM
- **CORS** - Cross-origin resource sharing
- **UUID** - Unique ID generation

### Frontend
- **React 18** - UI library
- **Vite** - Build tool and dev server
- **Axios** - HTTP client
- **CSS3** - Styling

### Infrastructure
- **Docker** - Containerization
- **Nginx** - Reverse proxy and load balancer
- **Docker Compose** - Multi-container orchestration

### DevOps
- **Bitbucket Pipelines** - CI/CD automation
- **MongoDB Backup Scripts** - Database backup utilities

## Project Structure

```
project-root/
├── backend/              # Node.js Express API
│   ├── package.json
│   ├── server.js
│   ├── Dockerfile
│   └── .dockerignore
├── frontend/             # React application
│   ├── package.json
│   ├── vite.config.js
│   ├── index.html
│   ├── nginx.conf
│   ├── Dockerfile
│   ├── .dockerignore
│   └── src/
│       ├── main.jsx
│       ├── App.jsx
│       └── index.css
├── nginx/                # Reverse proxy configuration
│   ├── Dockerfile
│   ├── nginx.conf
│   └── conf.d/
│       └── default.conf
├── mongodb/              # Database configuration
│   ├── Dockerfile
│   └── mongo-init.js
├── scripts/              # Utility scripts
│   ├── backup-mongodb.sh
│   └── backup-mongodb.bat
├── docker-compose.yml    # Production orchestration
├── docker-compose.dev.yml # Development orchestration
├── bitbucket-pipelines.yml # CI/CD configuration
└── package.json          # Root package.json
```

## Getting Started

### Prerequisites

#### Option 1: Local Development
- Node.js (v16 or higher)
- npm or yarn
- MongoDB (if running locally)

#### Option 2: Docker Development (Recommended)
- Docker
- Docker Compose

### Installation & Running

#### Docker Development (Recommended)

1. **Development Mode with Hot Reload:**
   ```bash
   docker-compose up --build
   ```
   
   This starts:
   - MongoDB on port 27017
   - Backend API on port 5000 (with nodemon)
   - Frontend dev server on port 3000 (with Vite HMR)
   - Nginx reverse proxy on port 80

2. **Production Mode:**
   ```bash
   docker-compose up --build
   ```
   
   This starts:
   - MongoDB (internal network)
   - Backend API (internal network)
   - Frontend (served by Nginx)
   - Nginx reverse proxy on port 80

#### Local Development

1. **Install all dependencies:**
   ```bash
   npm run install:all
   ```

2. **Start MongoDB locally** (or use Docker):
   ```bash
   docker run -d -p 27017:27017 --name mongodb mongo:7
   ```

3. **Run the application:**
   ```bash
   npm run dev
   ```

### API Endpoints

The backend provides the following REST API endpoints:

- `GET /api/todos` - Get all todos
- `POST /api/todos` - Create a new todo
- `PUT /api/todos/:id` - Update a specific todo
- `DELETE /api/todos/:id` - Delete a specific todo
- `GET /api/health` - Health check endpoint

### Production Build

#### Docker Production
```bash
docker-compose up --build -d
```

#### Local Production Build
```bash
npm run build:frontend
```

## Database Management

### MongoDB Backup

The project includes automated backup scripts for MongoDB:

**Linux/Mac:**
```bash
./scripts/backup-mongodb.sh [backup_name]
```

Backups are stored in the `./backups` directory and include:
- Compressed archive of the database
- Timestamp-based naming
- Automatic cleanup of temporary files

### Database Connection

The application connects to MongoDB using:
- **Development**: `mongodb://todouser:todopass@localhost:27017/todoapp`
- **Production**: `mongodb://todouser:todopass@mongodb:27017/todoapp`

## CI/CD Pipeline

The project includes a comprehensive Bitbucket Pipelines configuration:

### Pipeline Features:
- **Parallel execution** for faster builds
- **Automated testing** with MongoDB service
- **Security scanning** with npm audit
- **Docker image building** for all services
- **Integration testing** with full stack
- **Automated deployments** to staging/production

### Branch Strategy:
- **develop** → Automatic staging deployment
- **master** → Manual production deployment
- **pull-requests** → Validation pipeline
- **tags (v*)** → Release pipeline

## Usage

1. **Add a Todo**: Type in the input field and click "Add Todo" or press Enter
2. **Complete a Todo**: Click the checkbox next to a todo item
3. **Edit a Todo**: Click the "Edit" button, modify the text, and click "Save"
4. **Delete a Todo**: Click the "Delete" button next to a todo item

## Features in Detail

### CRUD Operations
- **Create**: Add new todo items with validation
- **Read**: Display all todos with completion status
- **Update**: Edit todo text and toggle completion status
- **Delete**: Remove todos permanently

### User Interface
- Clean, modern design
- Responsive layout for mobile and desktop
- Real-time feedback for user actions
- Error handling and loading states
- Todo completion statistics

### Infrastructure Features
- **Containerized Architecture**: Full Docker support with multi-stage builds
- **Reverse Proxy**: Nginx for load balancing and SSL termination
- **Database Persistence**: MongoDB with automated backups
- **Health Checks**: Built-in health monitoring for all services
- **Development Tools**: Hot reload for both frontend and backend
- **Security**: Non-root containers, security headers, and audit scanning

## Architecture

```
Internet → Nginx (Port 80) → Frontend (React)
                         ↓
                    Backend API (Express) → MongoDB
```

### Service Communication:
- **Frontend**: Served by Nginx or Vite dev server
- **API Routes**: Proxied through Nginx to backend
- **Database**: MongoDB with connection pooling
- **Networking**: Docker bridge network for service isolation

## Environment Variables

### Backend
- `NODE_ENV`: Environment mode (development/production)
- `PORT`: Server port (default: 5000)
- `MONGODB_URI`: Database connection string

### Frontend
- `VITE_API_URL`: Backend API URL for development

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Make your changes
4. Run tests and ensure Docker builds work
5. Commit your changes (`git commit -m 'Add amazing feature'`)
6. Push to the branch (`git push origin feature/amazing-feature`)
7. Open a Pull Request

### Development Guidelines
- Follow the existing code style
- Add tests for new features
- Update documentation as needed
- Ensure Docker containers build successfully
- Run security scans before submitting

## Deployment

### Staging
Automatic deployment on push to `develop` branch via Bitbucket Pipelines.

### Production
Manual deployment on push to `master` branch with approval gate.

### Manual Deployment
```bash
# Production
docker-compose up -d

# Development
docker-compose -f docker-compose.dev.yml up -d
```

## Monitoring & Maintenance

### Health Checks
- **Nginx**: `GET /health`
- **Backend**: `GET /api/health`
- **MongoDB**: Built-in health monitoring
- **Frontend**: Automatic availability checks

### Logs
```bash
# View all service logs
docker-compose logs -f

# View specific service logs
docker-compose logs -f backend
docker-compose logs -f frontend
docker-compose logs -f nginx
docker-compose logs -f mongodb
```

### Backup Schedule
- Manual backups via scripts in `./scripts/`
- Automated backups can be scheduled via cron/task scheduler
- Backups stored in `./backups/` directory

## License

This project is licensed under the MIT License.
