# List of Docker images

> Docker images from Docker hub used often to run services without changing local machine configuration

## MongoDB

[MongoDB](https://www.mongodb.com/fr) service from official [image](https://hub.docker.com/_/mongo) :
```bash
docker run -d -p 27017:27017 -v -v <path_to_a_local_folder>:/data/db --name <your_favorite_image_name> mongo:latest
```

where :
- `-d` : runs in detached mode, is equal to `-d=true`
- `-p 27017:27017` : maps container 27017 port to local 27017, to change if you already have a local mongo service
- `-v <path_to_a_local_folder>:/data/db` : Creates a [volume](https://docs.docker.com/storage/volumes/) to persist container datas on your local machine
- `--name <your_favorite_image_name>` : Your service name, choose wisely to facilitate maintenance
- `mongo:latest` : Official image latest version

## Mailcatcher

Initializes a SMTP server which catches any message sent to it to display in a web interface, [tophfr](https://hub.docker.com/r/tophfr/mailcatcher) image :
```bash
docker run -d -p 1080:80 -p 1025:25 --name mailcatcher tophfr/mailcatcher
```

where :
- `-d` : runs in detached mode, is equal to `-d=true`
- `-p 1080:80` : maps container 80 port to local 1080, the service client
- `-p 1025:25` : maps container 25 port to local 1025, the smtp server
- `--name <your_favorite_image_name>` : Your service name, choose wisely to facilitate maintenance
- `tophfr/mailcatcher` : Image name
