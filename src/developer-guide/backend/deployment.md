# Deployment

This documentation provides instructions for deploying the backend of the JSON-maker application using Docker Compose. The deployment includes multiple services orchestrated by Docker containers and relies on Docker, MongoDB, and REDCap.

## Services

The backend consists of the following services:

1. `frontend`: A React + TypeScript frontend for the JSON-maker application.
2. `api`: A RUST server built with Rocket framework, which includes integration with REDCap and provides an endpoint for MongoDB.
3. `caddy`: A web server and reverse proxy server that acts as a load balancer, TLS terminator, and HTTP/2 server.

## Docker Compose Configuration

The deployment is defined in a Docker Compose file that describes the multi-container architecture. The configuration consists of three services:

1. `caddy`: Based on the `lucaslorentz/caddy-docker-proxy:ci-alpine` Docker image, this service serves as a reverse proxy for other services. It listens on ports 80 and 443 and is configured with the `CADDY_INGRESS_NETWORKS` environment variable to specify the allowed networks. It is connected to the `caddy` network and mounts the Docker socket and a volume named `caddy_data` for storing configuration files.

2. `api`: This service is built from the Dockerfile located in the `./api` directory. It is connected to the `caddy` network, mounts the `./api` directory as a volume, and is labeled with caddy configuration information. The API listens on port 8000 and is reverse proxied by caddy at the `/api/*` path.

3. `web`: This service is built from the Dockerfile located in the `./frontend` directory. It is connected to the `caddy` network, listens on port 3000, and is reverse proxied by caddy at the root path. The service is also labeled with caddy configuration information.

## Reproduction Steps

Before deploying the backend on your server, ensure that you have Docker, MongoDB, and REDCap installed.

1. Install Docker by following the instructions at [https://docs.docker.com/get-docker/](https://docs.docker.com/get-docker/).

2. Install MongoDB by referring to the MongoDB installation documentation at [https://www.mongodb.com/docs/manual/installation/](https://www.mongodb.com/docs/manual/installation/).

3. Install REDCap, which is server software, by following the requirements and installation instructions provided at [https://projectredcap.org/software/requirements/](https://projectredcap.org/software/requirements/). Note that REDCap is not installed on a personal computer but on a server.

4. Update MongoDB Connection URL: Open the `api/Rocket.toml` file and replace the `{YOUR_URL}` placeholder in the MongoDB connection URL with the appropriate URL for your MongoDB instance.

5. Set REDCap Super API Token: Create a file named `.env` inside the `api` directory. In the `.env` file, add the following line, replacing `ABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZ` with your actual REDCap super API token:

   ```plaintext
   REDCAP_SUPER_API_TOKEN=ABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZ
   ```

6. Start Docker: Ensure that Docker is running on your server by running the following command:

   ```plaintext
   docker info
   ```

   If Docker is active, proceed to the next step. If not, start Docker using the appropriate command for your operating system.

7. Deployment with Docker Compose: Run the following script for development deployment:

   ```plaintext
   docker network create caddy
   docker compose -f docker-compose.local.yml up --build -d
   ```

   This command starts the services as close to production as possible but makes them available on localhost rather than the normal domain.

8. Clean Docker Cache (optional): Docker may consume a significant amount of disk space with build cache. To clean up the cache, run the following command and confirm with `y`:

   ```plaintext
   docker system prune
   ```

9. Manual Run: To run the services manually, follow these steps:

   - Frontend:
     ```Shell
     cd frontend
     pnpm
     pnpm dev
     ```
     Note: `pnpm` is used for its advantages in terms of speed and disk space efficiency. Install pnpm by running 
     ``` Shell 
     npm install -g pnpm
     ``` 
     (you may need superuser rights for this command, also refer to this guide for more information about installation - [Deployment](../designer/deployment.md)).

   - Rust API:
     ```Shell
     cd api
     cargo watch -x run
     ```
     Development:
     ```Shell
     cd api
     cargo watch -x run
     ```
     Production:
     ```Shell
     cd api
     cargo run --release
     ```

   - Alternatively, you can use npm to install dependencies (`npm run dev` for the start script). To install yarn, run `npm install -g yarn` (you may need superuser rights for this command).

## Production Deployment

For production deployment, follow these steps:

1. Clone the `_momenTUM-json-maker` repository if you don't have it in your userspace:

   ```plaintext
   git clone <repository_url>
   ```

2. Navigate to the `_momenTUM-json-maker` directory.

3. Pull the latest changes from GitHub, create the `caddy` network, and start the Docker containers:

   ```plaintext
   git pull && docker network create caddy && docker compose up -d --build
   ```

   This command automatically pulls the latest changes, builds the project for production, and starts the Docker containers.

4. Access the Project: You can now access the JSON-maker project at `https://make.momentumresearch.eu`, and the API is available at `https://make.momentumresearch.eu`.

Note: The production deployment assumes the availability of appropriate domain names and TLS certificates for HTTPS access. Ensure that you have configured the necessary DNS settings and obtained valid TLS certificates before deploying to production.