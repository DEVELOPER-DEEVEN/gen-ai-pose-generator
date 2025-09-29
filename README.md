# gen-ai-pose-generator

A production-ready, full-stack application for generating human pose images via Google Cloud's Imagen generative AI, powered by a Java/Spring Boot backend and a modern web frontend.

---

## Table of Contents

- [Features](#features)
- [Codebase Details](#codebase-details)
- [Installation Guide](#installation-guide)
- [Configuration](#configuration)
- [Usage](#usage)
- [API Reference](#api-reference)
- [Contributing](#contributing)
- [License](#license)
- [Acknowledgements](#acknowledgements)

---

## Features

- **AI-Driven Pose Generation:** Generate human pose images using Google Cloud’s Imagen model.
- **REST API:** Well-documented endpoints for job submission, status, and result retrieval.
- **Interactive Web UI:** Responsive web client for uploading prompts and visualizing results.
- **Customizable Output:** Support for pose type, style, and output format selection (PNG, JPEG, SVG).
- **Job Management:** Asynchronous processing and job status tracking.
- **Secure and Scalable:** Google Cloud IAM, environment-based secrets, role-based access.
- **Robust Error Handling:** Clear error messages for API and UI failures.
- **Extensible:** Modular codebase for easy feature addition.

---

## Codebase Details

### Technology Stack
- **Backend:** Java 17+, Spring Boot
- **Frontend:** HTML5, CSS3, JavaScript (Vanilla or with a framework)
- **Cloud Integration:** Google Cloud Vertex AI (Imagen), Google Cloud Storage
- **Build Tools:** Maven or Gradle

### Folder Structure (typical)
```
gen-ai-pose-generator/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/
│   │   │       └── yourorg/
│   │   │           └── posegen/
│   │   │               ├── controller/
│   │   │               ├── service/
│   │   │               ├── model/
│   │   │               └── ... 
│   │   ├── resources/
│   │   │   ├── application.properties
│   │   │   └── static/ (frontend files if not separate)
│   └── test/
│       └── java/...
├── frontend/ (if separate, else use static/)
├── pom.xml / build.gradle
└── README.md
```

### Main Components

- **Controller:** REST API endpoints for pose generation.
- **Service:** Business logic to call Google Cloud APIs, manage jobs, and process requests.
- **Model:** Data transfer objects (DTOs) and response wrappers.
- **Frontend:** Static assets for the web UI, or a separate `frontend/` directory if using a JS framework.

---

## Installation Guide

### 1. Prerequisites

- Java JDK 17 or newer
- Maven 3.8+ or Gradle 7+
- Google Cloud account with Vertex AI and Storage APIs enabled
- Google Cloud SDK (`gcloud`) installed and authenticated
- Node.js & npm (only for separate frontend development)
- Git

### 2. Clone the Repository

```bash
git clone https://github.com/DEVELOPER-DEEVEN/gen-ai-pose-generator.git
cd gen-ai-pose-generator
```

### 3. Google Cloud Setup

1. **Create a GCP Project:**  
   Go to [Google Cloud Console](https://console.cloud.google.com/), create a project.

2. **Enable APIs:**  
   Enable "Vertex AI" and "Cloud Storage" APIs for your project.

3. **Create Service Account:**  
   - Assign `Vertex AI User` and `Storage Object Admin` roles.
   - Download the service account JSON key file.

4. **Set Environment Variable:**  
   ```bash
   export GOOGLE_APPLICATION_CREDENTIALS="/absolute/path/to/service-account.json"
   ```

### 4. Configure Application

Edit `src/main/resources/application.properties` and set:
```properties
gcp.project-id=your-gcp-project-id
ai.imagen.model=imagen-v3
storage.bucket.name=your-storage-bucket
server.port=8080
```
Or use environment variables.

### 5. Build and Run Backend

#### Using Maven
```bash
mvn clean package
java -jar target/gen-ai-pose-generator-*.jar
```

#### Using Gradle
```bash
./gradlew bootRun
```

Backend will be available at `http://localhost:8080/`.

### 6. (Optional) Build Frontend

If frontend is separate:
```bash
cd frontend
npm install
npm run build
npm start
```
Otherwise, static files are served by Spring Boot.

### 7. Verify Setup

- Visit `http://localhost:8080/`
- Use the web UI or test API endpoints with Postman/curl.

---

## Configuration

| Property / Env Var              | Description                        | Example                         |
|----------------------------------|------------------------------------|---------------------------------|
| `GOOGLE_APPLICATION_CREDENTIALS` | Path to GCP service account key    | `/home/user/gcp-key.json`       |
| `gcp.project-id`                 | GCP project ID                     | `my-gcp-project`                |
| `ai.imagen.model`                | Imagen model version               | `imagen-v3`                     |
| `storage.bucket.name`            | GCS bucket for outputs             | `genai-pose-outputs`            |
| `server.port`                    | Application port                   | `8080`                          |

---

## Usage

### Web UI

- Access `http://localhost:8080/`
- Upload prompt or select pose options, submit generation request
- Wait for processing, view or download results

### API Example

- **POST /api/v1/poses/generate**
    ```json
    {
      "prompt": "person dancing, arms raised",
      "outputFormat": "png"
    }
    ```
- **GET /api/v1/poses/status/{jobId}**
- **GET /api/v1/poses/result/{jobId}**

---

## API Reference

| Method | Endpoint                        | Description                     |
|--------|---------------------------------|---------------------------------|
| POST   | `/api/v1/poses/generate`        | Submit pose generation request  |
| GET    | `/api/v1/poses/status/{jobId}`  | Check job status                |
| GET    | `/api/v1/poses/result/{jobId}`  | Download generated image        |

See `/docs` endpoint (if enabled) or code for detailed specs.

---

## Contributing

1. Fork the repo
2. Create a branch (`git checkout -b feature/your-feature`)
3. Commit your changes
4. Push the branch
5. Open a Pull Request

Open issues for bugs/feature requests. All contributions welcome!

---

## License

Licensed under the [Apache License 2.0](LICENSE).

---

## Acknowledgements

- Google Cloud AI/ML
- Spring Boot Community
- All contributors

---

## Resources

- [Google Cloud Vertex AI](https://cloud.google.com/vertex-ai)
- [Spring Boot](https://spring.io/projects/spring-boot)
- [Repository](https://github.com/DEVELOPER-DEEVEN/gen-ai-pose-generator)
