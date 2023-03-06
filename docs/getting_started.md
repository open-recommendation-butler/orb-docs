# Getting started

## Installation

You can start ORB on your machine with docker by following these steps:

- Clone the repository

```bash
git clone https://github.com/open-recommendation-butler/ORB.git
```

- Change directory to project directory

```bash
cd ORB
```

- Create a file with the name ".env".

- Insert the following content into the ".env" file. Replace *YourStrongPasswordForElasticSearch*, *YourStrongPasswordForKibana* and *YourStrongSecretKeyForDjango* with your own passwords.

Content of ".env" file:
```bash
# Password for the 'elastic' user (at least 6 characters)
ELASTIC_PASSWORD=YourStrongPasswordForElasticSearch

# Password for the 'kibana_system' user (at least 6 characters)
KIBANA_PASSWORD=YourStrongPasswordForKibana

# Secret key for Django (at least 6 characters)
SECRET_KEY=YourStrongSecretKeyForDjango
```

- Compose the docker
```bash
docker compose build
```

- Compose the docker
```bash
docker compose up -d
```

- Test if ORB is running by visiting [http://localhost:8000](http://localhost:8000).