# Notes REST API – Dockerized Microservices Project

A full-stack backend project demonstrating **Docker**, **Node.js / Express**, **MongoDB**, and **Nginx**.  
The application exposes a REST API for managing notebooks and notes, running as multiple services orchestrated with Docker Compose.

---

## Project Overview

This project shows how to:

- **Code a notes REST API** with two microservices:  
  - `notebooks` service  
  - `notes` service  
  - plus a reverse proxy (Nginx)
- **Create and manage multiple Compose projects** for modular development.
- **Leverage Docker Compose merge functionality** to integrate and manage services simultaneously.
- **Handle service outages and improve resiliency** by designing APIs that tolerate dependent-service failures.

---

## Tech Stack

- **Docker & Docker Compose** – containerization and orchestration
- **Node.js / Express.js** – REST API services
- **MongoDB** – persistent data store
- **Nginx** – reverse proxy and load balancer

---

## API Specifications

### Notebooks Service

| Method & Path            | Behavior |
|--------------------------|---------|
| **POST** `/api/notebooks` | Requires `name` in body (optional `description`). Creates a notebook. Returns **201** or **400** if invalid. |
| **GET** `/api/notebooks`  | Returns all notebooks. |
| **GET** `/api/notebooks/:id` | Returns notebook by id or **404** if not found. |
| **PUT** `/api/notebooks/:id` | Updates notebook if id exists (**200**), else **404**. |
| **DELETE** `/api/notebooks/:id` | Deletes notebook if id exists (**204**), else **404**. |
| **GET** `/health`         | Health-check endpoint, returns **200** with text `up`. |

### Notes Service

| Method & Path        | Behavior |
|----------------------|---------|
| **POST** `/api/notes` | Requires `title` and `content` in body. Optional `notebookId`. Returns **201** or **400** if invalid. If `notebookId` is supplied but notebooks service is down, still stores note with provided id. |
| **GET** `/api/notes`  | Returns all notes. |
| **GET** `/api/notes/:id` | Returns note by id or **404** if not found. |
| **PUT** `/api/notes/:id` | Updates note if id exists (**200**), else **404**. |
| **DELETE** `/api/notes/:id` | Deletes note if id exists (**204**), else **404**. |
| **GET** `/health`     | Health-check endpoint, returns **200** with text `up`. |

## Running Locally

1. **Clone the repository**

   ```bash
   git clone https://github.com/anishkumar63588/Notes-REST-API-Dockerized-Microservices-Project.git
   cd notes-rest-api