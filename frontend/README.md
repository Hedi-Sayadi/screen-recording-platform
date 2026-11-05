# Browser Screen Recording Platform

Browser-based screen recording application built with Angular and Spring Boot. It captures the selected screen and microphone audio in the browser, previews the recording, uploads video files, and lists stored recordings.

## Features

- Capture screen video with the browser MediaDevices API
- Capture microphone audio and combine it with the screen stream
- Record WebM video with RecordRTC
- Preview recordings before upload
- Upload local video files
- Browse recordings stored in Azure Blob Storage or the Azurite emulator

## Architecture

The project is maintained across two branches:

| Branch | Contents |
| --- | --- |
| `front` | Angular client application |
| `backend` | Spring Boot REST API and Azure Blob Storage integration |

The frontend communicates with the backend through the `/video` API:

```text
Browser
   |
   v
Angular client (:80 or :4200)
   |
   v
Spring Boot API (:8080)
   |
   v
Azure Blob Storage / Azurite
```

## Prerequisites

- Node.js and npm
- Java 17
- Docker and Docker Compose
- A modern browser with screen-capture support

## Frontend development

```bash
npm install
npm start
```

Open <http://localhost:4200>. The development environment expects the backend at `http://localhost:8080/video`.

Build the production bundle:

```bash
npm run build
```

## Backend development

Switch to the `backend` branch and follow its README for Spring Boot and Azure Storage setup:

```bash
git switch backend
./mvnw spring-boot:run
```

On Windows, use `mvnw.cmd spring-boot:run`.

## Docker

The frontend Dockerfile builds the Angular application and serves it with Nginx. The backend branch contains the Spring Boot Dockerfile and the local Azurite service configuration.

## Configuration

The frontend API URL is configured in:

- `src/environments/environment.ts`
- `src/environments/environment.prod.ts`

The backend storage connection is configured through an environment variable. Use the backend branch's `.env.example` as the local configuration template.
