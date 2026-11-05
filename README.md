# Screen Recording Platform

Browser-based screen recording platform built with Angular and Spring Boot. The frontend captures screen and microphone input, while the backend stores and streams WebM recordings through Azure Blob Storage or the local Azurite emulator.

## Architecture

```text
Browser
   |
   v
Angular frontend (:80 or :4200)
   |
   v
Spring Boot API (:8080)
   |
   v
Azure Blob Storage / Azurite
```

## Project structure

```text
.
├── frontend/   Angular client
└── backend/    Spring Boot REST API
```

## Features

- Capture the selected screen and microphone audio in the browser
- Preview recordings before upload
- Upload local video files
- Store and stream WebM recordings
- Run locally with the Azurite Azure Storage emulator
- Build both applications with Docker

## Prerequisites

- Node.js and npm
- Java 17
- Docker and Docker Compose
- A modern browser with screen-capture support

## Frontend

```bash
cd frontend
npm install
npm start
```

Open <http://localhost:4200>. The frontend expects the API at `http://localhost:8080/video`.

Build the Angular application:

```bash
npm run build
```

## Backend

```bash
cd backend
copy .env.example .env
mvnw.cmd spring-boot:run
```

On macOS or Linux, use `cp .env.example .env` and `./mvnw spring-boot:run`.

The API is available at <http://localhost:8080>.

### API endpoints

| Method | Endpoint | Purpose |
| --- | --- | --- |
| `POST` | `/video/upload` | Upload a video using the `file` multipart field |
| `GET` | `/video/videoBlobStorage` | List stored video names |
| `GET` | `/video/{videoName}` | Stream a stored video |

## Docker

Run the backend with the local Azurite emulator:

```bash
cd backend
docker compose -f docker-compose-front-back.yaml up --build
```

The frontend Dockerfile builds the Angular application and serves it with Nginx. The backend storage connection is configured with `AZURE_STORAGE_CONNECTION_STRING` in `backend/.env`.

## Configuration

The frontend API URL is configured in `frontend/src/environments/`. The backend uses `backend/.env.example` as the template for Azure Blob Storage or Azurite configuration.
