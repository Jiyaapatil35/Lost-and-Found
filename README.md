# Lost and Found

## Overview

Lost and Found is a full-stack platform that enables users to register, log in, upload lost or found items, and manage item notifications. The project combines a React frontend with a Node.js/Express backend, MongoDB persistence, and observability via Prometheus and Grafana.

## Key Features

- User authentication and authorization
- Upload and manage lost items
- Upload and manage found items
- Item notifications and alerts
- File upload support for item images
- Prometheus metrics exposed from the backend
- Docker Compose orchestration for local deployment
- Jenkins pipeline for automated build and deployment

## Architecture

- `backend/` - Node.js API server with Express, MongoDB, JWT authentication, and file upload handling.
- `frontend/` - React application built with Vite, Tailwind CSS, and React Router.
- `docker-compose.yml` - Orchestrates MongoDB, backend, frontend, Prometheus, and Grafana.
- `prometheus.yml` - Prometheus configuration to scrape backend metrics.
- `Jenkinsfile` - CI/CD pipeline that builds and starts Docker containers.

## Prerequisites

- Docker and Docker Compose
- Node.js (if running locally without Docker)
- npm or yarn
- Jenkins (optional, for CI/CD)

## Getting Started

### Run with Docker Compose

1. From the project root:

```bash
docker compose up --build -d
```

2. Access services:

- Frontend: `http://localhost:5173`
- Backend API: `http://localhost:5000`
- Prometheus: `http://localhost:9090`
- Grafana: `http://localhost:3000`

### Run Backend Locally

1. Navigate to the backend folder:

```bash
cd backend
npm install
```

2. Create a `.env` file with values for:

- `MONGODB_URI`
- `PORT`
- `JWT_SECRET`
- `BASE_URL`

3. Start the backend server:

```bash
npm start
```

### Run Frontend Locally

1. Navigate to the frontend folder:

```bash
cd frontend
npm install
```

2. Create a `.env` file or set `VITE_API_URL` to the backend API endpoint.

3. Start the frontend development server:

```bash
npm run dev
```

## Environment Variables

### Backend

- `MONGODB_URI` - MongoDB connection string
- `PORT` - Server port (default: `5000`)
- `JWT_SECRET` - Secret key for JSON Web Tokens
- `BASE_URL` - Backend base URL

### Frontend

- `VITE_API_URL` - Backend API base URL used by the React app

### Docker Compose Example

The project `docker-compose.yml` already defines environment values for local container deployment, including:

- `MONGODB_URI=mongodb://mongodb:27017/lost-and-found`
- `PORT=5000`
- `JWT_SECRET=my_super_secret_jwt_key_123`
- `BASE_URL=http://16.192.57.191:5000`
- `VITE_API_URL=http://16.192.57.191:5000/api`

> Update these values for your production or local environment as needed.

## Monitoring

- Backend exposes Prometheus metrics at `/metrics`
- Prometheus is configured in `prometheus.yml`
- Grafana is available on port `3000` with default admin credentials configured in the compose file

## CI/CD

- `Jenkinsfile` defines a pipeline that:
  - clones the repository
  - removes old containers
  - builds Docker images
  - starts containers with Docker Compose
  - verifies the deployment

## Folder Structure

- `backend/`
  - `controllers/` - Request handlers for auth, items, and notifications
  - `middlewares/` - Authentication and upload middleware
  - `models/` - Mongoose schemas
  - `routes/` - API route definitions
  - `utils/` - Cloudinary integration and token generation
- `frontend/`
  - `components/` - UI components such as navigation and sidebar
  - `context/` - Authentication context provider
  - `pages/` - Application pages for landing, login, dashboard, and item management
  - `utils/` - API helper functions

## Contribution

Contributions are welcome. For issues or improvements, please open a pull request or issue in the repository.

## License

This repository does not specify a license. Add a license file if you intend to publish or share this project publicly.
