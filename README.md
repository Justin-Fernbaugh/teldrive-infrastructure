# teldrive-infrastructure
# Docker Compose for Teldrive and PostgreSQL

This repository contains a `docker-compose.yml` file to set up and run the Teldrive server along with a PostgreSQL database using Docker Compose.

## Services

The `docker-compose.yml` file defines two services:

1. **server**: This is the Teldrive server service.
2. **db**: This is the PostgreSQL database service.

### server

- **Image**: `ghcr.io/divyam234/teldrive`
- **Container Name**: `teldrive`
- **Environment Variables**:
  - `home`: Set to `/`
- **Volumes**:
  - `./session.db:/session.db:rw`: Mounts the `session.db` file from the host to the container.
  - `./config.toml:/.teldrive/`: Mounts the `config.toml` file from the host to the container.
- **Ports**:
  - `8080:8080`: Maps port 8080 on the host to port 8080 on the container.

### db

- **Image**: `postgres:latest`
- **Container Name**: `postgres_db`
- **Environment Variables**:
  - `POSTGRES_DB`: Set to `mydatabase`
  - `POSTGRES_USER`: Set to `myuser`
  - `POSTGRES_PASSWORD`: Set to `mypassword`
- **Volumes**:
  - `pgdata:/var/lib/postgresql/data`: Creates a named volume `pgdata` to persist PostgreSQL data.
- **Ports**:
  - `5432:5432`: Maps port 5432 on the host to port 5432 on the container.

## Volumes

- **pgdata**: A named volume for persisting PostgreSQL data.

## Running the Services

To run the services using Docker Compose, follow these steps:

1. **Ensure Docker and Docker Compose are installed**:

   - [Install Docker](https://docs.docker.com/get-docker/)
   - [Install Docker Compose](https://docs.docker.com/compose/install/)

2. **Clone the Repository**:

   ```bash
   git clone <repository_url>
   cd <repository_directory>
   ```
3. **Create Required Files**:
  ```bash
  touch session.db
  touch config.toml
  ```

4. **Build the Docker Images**:
  ```bash
  docker-compose build
  ```

5. **Run Docker Compose**:
  ```bash
  docker-compose up -d
  ```

6. **Verify the Services are Running**:
  ```bash
  docker-compose ps
  ```

7. **Server is ready on localhost**:
- The server can be accessed as http://localhost:8080
- The PostgreSQL database is also available at localhost:5432
- From here port 8080 can either be exposed or configured with a reverse proxy on port 80 and 443 using SSL.

