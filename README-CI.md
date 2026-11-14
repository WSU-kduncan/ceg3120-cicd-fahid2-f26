# Project 6 - CI

## Part 1 - Docker Container Image

### Website Content

For this project, I reused the website files that I created during Project 5. The website contains the two HTML pages, index.html and about.html, along with style.css


### Docker

I created a Dockerfile using these:

```dockerfile
FROM httpd:2.4
COPY web-content/ /usr/local/apache2/htdocs/
```

I built the image using:

```bash
docker build -t rababaf/cicd:1.0 .
```

I ran the image using:

```bash
docker run -d --name fahid-webserver -p 8090:80 rababaf/cicd:1.0
```

### DockerHub

I created a public DockerHub repository and logged in using a Personal Access Token with read and write permissions and a 90 day expiration.

I pushed the image using:

```bash
docker push rababaf/cicd:1.0
```

DockerHub repository: 

```https://hub.docker.com/r/rababaf/cicd```

### Testing

I tested the running container using:

```bash
docker ps
```
Accessing the web pages:

- http://localhost:8090/
- http://localhost:8090/about.html

