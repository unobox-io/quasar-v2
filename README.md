# Quasar Docker

## Getting Started (Development)

1. Create the file ./docker-compose.override.yml using ./.docker-compose.override.yml.dist
2. If not already done, [install Docker Compose](https://docs.docker.com/compose/install/)
3. Run `docker compose build` to build fresh images
4. Run `docker compose up`
5. Open `http://localhost:3000` in your web browser
6. Run `docker compose down --remove-orphans` to stop the Docker containers.
