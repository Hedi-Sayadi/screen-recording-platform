# Browser Screen Recording API

Spring Boot REST API for storing and retrieving browser screen recordings in Azure Blob Storage. It is the backend for the Angular client on the `front` branch.

## Features

- Upload WebM recordings through a multipart endpoint
- List stored recordings
- Stream stored recordings back to the browser
- Run locally with the Azurite Azure Storage emulator
- Package as a Java 17 Docker image

## API

| Method | Endpoint | Purpose |
| --- | --- | --- |
| `POST` | `/video/upload` | Upload a video using the `file` multipart field |
| `GET` | `/video/videoBlobStorage` | List stored video names |
| `GET` | `/video/{videoName}` | Stream a stored video |

The Angular client expects the API at `http://localhost:8080/video`.

## Prerequisites

- Java 17
- Docker and Docker Compose
- Maven wrapper (included)

## Run locally with Azurite

1. Copy `.env.example` to `.env`.
2. Start Azurite and the API:

   ```bash
   docker compose -f docker-compose-front-back.yaml up --build
   ```

3. The API is available at <http://localhost:8080>.

To run Spring Boot directly, start Azurite separately and set `AZURE_STORAGE_CONNECTION_STRING` to a connection string that uses `http://localhost:10000/devstoreaccount1` before running:

```bash
./mvnw spring-boot:run
```

On Windows, use `mvnw.cmd spring-boot:run`.

## Configuration

Storage configuration is supplied through `AZURE_STORAGE_CONNECTION_STRING`. The committed `.env.example` uses the standard local Azurite development account. Replace it with an Azure Blob Storage connection string when deploying outside local development.

## Project branches

- `front`: Angular screen-recording client
- `backend`: this Spring Boot API
