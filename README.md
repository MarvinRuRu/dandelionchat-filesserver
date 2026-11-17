# dandelionchat-filesserver

#### Settings file

```json
{
    "server_jwt_secret": "bfcjJe+xSa1IPsszJlvFRzbp78-I6HeqP54SaY713b4=",
    "files_base_path": "/opt/no_memory_chat_files/files",
    "max_file_size_mb": 50
}
````
*   **files_base_path:** path where to store files.
*   **server_jwt_secret:** a symmetric encryption key shared between the file server and the message server. It must be identical for both servers.
*   **max_file_size_mb:** max file size file server accepts or 0 if any.

#### Starting the server via fat-jar

Example run:
```sh
CONFIG="config/settings.json" PORT=8086 HOST="127.0.0.1" /usr/lib/jvm/java-21-openjdk-amd64/bin/java -jar dandelionserver_files.jar
```

Reserve proxy domain must be configured like for 📦 [Dandelion Server](https://github.com/MarvinRuRu/dandelionchat).
