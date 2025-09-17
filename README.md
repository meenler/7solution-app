# Hello API

This is a simple Go web application that responds with a greeting message.
The project demonstrates how to containerize a Go application using Docker
with a multi-stage build for optimized image size.

---

## Project Structure

```
hello-api/
├── go.mod
├── main.go
├── Dockerfile
└── README.md
```

- **go.mod**: Go module file defining dependencies and Go version.
- **main.go**: Main application file. Implements a simple HTTP server.
- **Dockerfile**: Docker configuration file with multi-stage build.
- **README.md**: Project documentation.

---

## Requirements

- Go 1.21 or later
- Docker

---

## Build and Run Locally

### Run without Docker

1. Install dependencies:
   ```bash
   go mod tidy
   ```

2. Build and run:
   ```bash
   go run main.go
   ```

3. Test the API:
   ```bash
   curl "http://localhost:8080/?name=World"
   ```

Expected output:
```
Hello World
```

---

### Build and Run with Docker

1. Build the image:
   ```bash
   docker build -t hello-api .
   ```

2. Run the container:
   ```bash
   docker run -p 8080:8080 hello-api
   ```

3. Test the API:
   ```bash
   curl "http://localhost:8080/?name=Peerasilp"
   ```

Expected output:
```
Hello Peerasilp
```

---

## Dockerfile Explanation

The Dockerfile uses a **multi-stage build**:

1. **Builder stage** (`golang:1.21`):
   - Compiles the Go application into a binary.

2. **Runtime stage** (`debian:bookworm-slim`):
   - Copies only the binary from the builder stage.
   - Keeps the final image small and secure.

---

## API Endpoints

- `GET /`  
  **Query Parameters**:  
  - `name` (string): Name to greet.

**Example**:
```
curl "http://localhost:8080/?name=Alice"
```
Response:
```
Hello Alice
```

---

## License

