# dandelionchat-filesserver

### Setting Up and Running the Server

#### 1. Fill in the server configuration file settings.json

```json
{
    "server_jwt_secret": "bfcjJe+xSa1IPsszJlvFRzbp78-I6HeqP54SaY713b4=",
    "files_base_path": "/opt/dandelionchat_files/files",
    "max_file_size_mb": 50
}
````
*   **files_base_path:** path where to store files.
*   **server_jwt_secret:** a symmetric encryption key shared between the file server and the message server. It must be identical for both servers.
*   **max_file_size_mb:** max file size file server accepts or 0 if any.

#### 2. Start the server

#### Environment variables for starting the server

* **PORT:** Port where the server will run
* **HOST:** Host where the server will run
* **CONFIG:** Path to the server configuration file

#### 2.1 Starting the server via fat-jar

Example run:
```sh
CONFIG="config/settings.json" PORT=8086 HOST="127.0.0.1" /usr/lib/jvm/java-21-openjdk-amd64/bin/java -jar dandelionserver_files.jar
```
#### 2.2 Starting the server from a Docker container

**docker-compose.yml** to start the server on port 8086, on a fixed IP address of 172.18.0.101 in the virtual network.

* it is assumed that the server configuration file is located at `config/settings.json` relative to `docker-compose.yml` 
* it is assumed that directory `files` exists relative to `docker-compose.yml` and `files_base_path` in `settings.json` is set to `/app/config`

```yaml
version: '3.8'

services:   
  files-server:
    image: zzhekaa/dandelionserver_files:latest
    container_name: dandelion-files-server
    ports:
      - "127.0.0.1:8086:8086"
    environment:
      - PORT=8086
      - HOST=0.0.0.0
      - CONFIG=/app/config/settings.json
    networks:
      dandelion-net:
        ipv4_address: 172.18.0.101
    volumes:
      - ./config_files:/app/config
      - ./files:/app/files
    restart: unless-stopped    

networks:
  dandelion-net:
    driver: bridge
    ipam:
      config:
        - subnet: 172.18.0.0/16

```

Running a container from a directory with docker-compose.yml:

```sh
docker-compose up -d
```


Reserve proxy domain must be configured as for 📦 [Dandelion Server](https://github.com/MarvinRuRu/dandelionchat) (as described in section 3 of the settings).
