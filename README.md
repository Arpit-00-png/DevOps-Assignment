# Task Management API

A Spring Boot REST API demonstrating DevOps practices.

## Technology Stack
- Java 17
- Spring Boot 3.3.5
- Maven
- Jenkins CI/CD
- Docker
- Ansible
- Kubernetes (Minikube)

## API Endpoints
- GET /
- GET /tasks
- GET /tasks/{id}
- POST /tasks
- GET /actuator/health

## CI/CD
Jenkins polls the GitHub main branch every two minutes, runs automated tests, builds the application, generates build version information, and archives the artifacts.
