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


## Part 2 - GitHub Actions

### Secrets

Two secrets were created in my Git repository. The process was done by going to Settings > Secrets and Variables. Also, the token which I generated is not pushed into my github repository according to the project guidelines due to security reasons. However, the token was utilized in the github Actions so the workflow logs in to Dockerhub and automates the workflow accordingly.

- `DOCKER_USERNAME` contains my DockerHub username.
- `DOCKER_TOKEN` contains my DockerHub PAT


### GitHub Actions Workflow

I created a workflow file named `docker-ci.yml` inside `.github/workflows/`. One issue I faced while pushing the `.github/workflows/`  was it was not authorized to be pushed. Therefore, I changed my permissions on github that included workflow as well. 
The workflow runs when I push a commit to the `main` branch.

The workflow contains four stages:

1. Checkout code - Gets the repository files.
2. Login - Logs in to DockerHub using GitHub Secrets in Actions.
3. Docker Buildx setup - Sets up Docker for creating the image.
4. Build and push - Builds the image using my Dockerfile and pushes it to DockerHub as `rababaf/cicd:latest`.


