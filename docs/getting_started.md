# Getting started

## Installation

You can start ORB on your machine with docker by following these steps:

1. Clone the repository

```bash
git clone https://github.com/open-recommendation-butler/ORB.git
```

2. Change directory to project directory

```bash
cd ORB
```

3. Create a file with the name ".env".

4. Insert the following content into the ".env" file. Replace *YourStrongPasswordForElasticSearch*, *YourStrongPasswordForKibana* and *YourStrongSecretKeyForDjango* with your own passwords.

Content of ".env" file:
```bash
# Password for the 'elastic' user (at least 6 characters)
ELASTIC_PASSWORD=YourStrongPasswordForElasticSearch

# Password for the 'kibana_system' user (at least 6 characters)
KIBANA_PASSWORD=YourStrongPasswordForKibana

# Secret key for Django (at least 6 characters)
SECRET_KEY=YourStrongSecretKeyForDjango
```

5. Compose the docker
```bash
docker compose build
```

6. Compose the docker
```bash
docker compose up -d
```

7. Test if ORB is running by visiting [http://localhost:8000](http://localhost:8000).


## How to add documents to the database?

After setting up the ORB docker, your database does not include any documents. Documents can be articles, podcasts, messages, newsletters etc.

In this tutorial you will learn how to add documents to the database.

### The API endpoint

ORB provides an API endpoint to add documents.

You can add articles by doing a POST request:

```bash
POST http://localhost:8000/article/
```

You can send the following data to the endpoint (as a JSON):
```json
{
  "title": "That's a title",
  "teaser": "That's a teaser",
  "fullext": "That's a fulltext",
  "url": "https://example.com/",
  "content_type": "article",
  "created": "2012-04-23T18:25:43.511Z"
}
```
None of the fields is mandatory.

If successful, the API sends the status *201 Created*.

### Examples

In this section you will find examples how to add send requests to the API.

#### a) Adding a document with Postman

You can add a document with [Postman](https://www.postman.com/). Postman is a program to test APIs.

Create a POST request, include the body as a JSON and send the document to the API as seen in the picture.

![Screenshot of a POST request in Postman](../1-adding-documents-to-the-database/add-document-w-postman.png "Add document with Postman")

#### b) Adding a document with Python

You can automate adding documents with the [Python Request Library](https://requests.readthedocs.io/en/latest/).

Install the library.

```bash
pip install requests
```

Run the following code to add a document:
```python
import requests

document = {
  "title": "That's a title",
  "teaser": "That's a teaser",
  "fullext": "That's a fulltext",
  "url": "https://example.com/",
  "content_type": "article",
  "created": "2012-04-23T18:25:43.511Z"
}

r = requests.post('http://localhost:8000/article/', json=document)

print(r.status_code)
```

## How to search for documents with the API?

You can use the web demo to search for documents ([http://localhost:8000](http://localhost:8000)) or you can use the API.

In the following, you will learn how to search with the API.

You can retrieve search results by sending a GET request:

```bash
GET http://localhost:8000/search/
```

You can use the following parameters:

| Parameter     | What it is        |
| ------------- |:-------------:|
| q      | Search term to query (string) |
| as_topics     | If results should be clustered in topics (boolean)      |
| return_json | If response should be JSON instead of HTML (boolean)      |

An example search would look like:
```
GET http://localhost:8000/search/?as_topics=True&q=der&return_json=True
```