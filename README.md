# NOTICE
- This FORK supports ARM for Apple M-series chip.
- Original repo: [oleduc's repo](https://github.com/oleduc/docker-obsidian-livesync-couchdb)

# CouchDB Configuration for Obsidian LiveSync

This repository provides a Docker container for configuring CouchDB specifically for use with [Obsidian LiveSync](https://github.com/vrtmrz/obsidian-livesync). It automates the setup process by parsing the bash script (`couchdb-init.sh`) provided by obsidian-livesync's maintainer and updating CouchDB's configuration file (`local.ini`) according to the settings the plugin needs.

The container is built and published automatically via GitHub Actions.

[Docker Hub Page](https://hub.docker.com/r/xarthur/obsidian-sync-couchdb)

## Features
- **Automated CouchDB Configuration**: Extracts necessary settings for Obsidian LiveSync from the bash script created by the plugin maintainer.
- **Build time configuration**: Configures couchDB at build time via configuration files instead of using couchDB APIs which simplifies the process.
- **Auto-Publishing**: Docker images are automatically built and pushed to a container registry via GitHub Actions.

## Pulling the Docker Image
To use the pre-built image, pull it from the container registry:
```bash
docker pull docker.io/xarthur/docker-obsidian-livesync-couchdb:latest
```

## Running the Container

### Command Line
```
docker run -d \
  -e SERVER_DOMAIN=example.com \
  -e COUCHDB_USER=username \
  -e COUCHDB_PASSWORD=password \
  -e COUCHDB_DATABASE=obsidian \
  -p 5984:5984 \
  docker.io/xarthur/docker-obsidian-livesync-couchdb:latest
```

### docker-compose
```yaml
version: "3.8"

services:
  couchdb-obsidian-livesync:
    container_name: couchdb-obsidian
    image: docker.io/xarthur/obsidian-sync-couchdb:latest
    environment:
      SERVER_URL: ${SERVER_URL}
      COUCHDB_USER: ${COUCHDB_USER}
      COUCHDB_PASSWORD: ${COUCHDB_PASSWORD}
      COUCHDB_DATABASE: ${COUCHDB_DATABASE}
    volumes:
      - ${COUCHDB_DATA}:/opt/couchdb/data
    ports:
      - "${COUCHDB_PORT:-5984}:5984"
    restart: unless-stopped
```

## Testing Configuration

To verify the updated configuration:

    Open your CouchDB dashboard (http://example.com:5984/_utils).
    Check that the settings are applied under /_node/_local/_config.

## License

This repository is licensed under the MIT License. Contributions are welcome!

## Credits

- [Obsidian LiveSync for the core synchronization functionality.](https://github.com/vrtmrz/obsidian-livesync)
- [CouchDB for its awesome, distributed database solution.](https://couchdb.apache.org/)
- [Obsidian for it's awesome note taking app.](https://obsidian.md/)
