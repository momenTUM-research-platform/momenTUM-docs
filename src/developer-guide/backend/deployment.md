# Deployment

The backend's design includes numerous services orchestrated by docker-compose in the form of docker containers. At the moment, the following services exist: 
- `frontend` directory contains the JSON-maker frontend, written in React + TypeScript. 
- `api` directory contains the JSON-maker server, written in RUST with Rocket as the web framework. It includes calling an Redcap instance to aggregate and funnels logs from the app to redcap. It also includes and endpoint for the mongodb. 
- [Caddy](https://github.com/caddyserver/caddy), which is a web server and reverse proxy server that offers a load balancer, TLS terminator, and HTTP/2 server. 

This is a Docker Compose file defining a multi-container application architecture that consists of three services: `caddy`, `api`, and `web`. The caddy service is based on the lucaslorentz/caddy-docker-proxy:ci-alpine Docker image and serves as a reverse proxy for the other services. It is configured to listen on ports 80 and 443 and uses the CADDY_INGRESS_NETWORKS environment variable to specify the networks it can communicate with. The service is connected to the caddy network and mounts the Docker socket and a volume named caddy_data for storing configuration files.

The `api` service is built from the Dockerfile located in the ./api directory and is also connected to the caddy network. It mounts the ./api directory as a volume and is labeled with caddy configuration information. This service listens on port 8000 and is reverse proxied by caddy at the /api/* path.

The `web` service is built from the Dockerfile located in the ./frontend directory and is also connected to the caddy network. It listens on port 3000 and is reverse proxied by caddy at the root path. The service is labeled with caddy configuration information as well.

## Steps to reprouce

### Requirements
For running the backend on your server, you have to install [Docker](https://docs.docker.com/get-docker/), [MongoDB](https://www.mongodb.com/docs/manual/installation/) and [REDCap](https://projectredcap.org/software/requirements/). 

Note: `REDCap` is server software. It is not something that a user installs on a personal computer

> ### Important: The `MongoDB` connection url and a `REDCap` super api token are required to continue after this step.



To set the `MongoDB` connection url, go inside the `\api\Rocket.toml` file and change this variable to your url.

```
...
[default.databases.mongodb]
url = "mongodb://{YOUR_URL}"
...
```

To set the `REDCap` super api token, then you need to create a `.env` file inside the `\api\` directory. The `\api\.env` file should look like:
```
REDCAP_SUPER_API_TOKEN=ABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZ
```

After installing docker, start your `docker` and check if docker is running by running this command:

```
docker info
```

If docker is active then run the following script for development:

```
docker network create caddy
docker compose -f docker-compose.local.yml  up --build -d
```

This will start your services as close to production as possible, just not available at the normal domain but on localhost.

Docker will eat up all your disk space with build cache, so you might want to clean it up from time to time. To do so, run `docker system prune` and confirm with `y`.

To run manually, install dependencies and run:

```
cd frontend
pnpm
pnpm dev
```

`pnpm` is used because of the advantages it has on Speed, and to save disk space. You can read more about `pnpm` [here](https://pnpm.io/). To install pnpm, run 
```
npm install -g pnpm
```
(Note: You might need superuser-rights for this command).

### Rust API

Install Rust: https://www.rust-lang.org/learn/get-started

Development

```
cd api
cargo watch -x run
```

Production

```
cd api
cargo run --release
```

Of course, you can also install dependencies with npm (then the start script is npm run dev). To install yarn, run 
```
npm install -g yarn
```
(Note: You might need superuser-rights for this command).


## Production

When deploying to production, cd into the _momenTUM-json-maker_ directory (clone it first if you don't have it in your userspace), then run 
```
git pull  && docker network create caddy  && docker compose up -d--build
``` 

which will automatically pull the latest changes from GitHub, build the project for production, and start the docker containers. You can then access the project at https://make.momentumresearch.eu. The API is running on https://make.momentumresearch.eu.


