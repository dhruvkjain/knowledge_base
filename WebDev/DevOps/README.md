
<details>
  <summary>CI/CD</summary>
  
# CI/CD
![Pasted image 20240605163256](https://github.com/user-attachments/assets/1e09275d-e460-446c-8854-5a09d4e91d93)

- [Continuous Integration and Delivery - CircleCI](https://circleci.com/)
- [Jenkins](https://www.jenkins.io/)
- [GitHub Actions documentation - GitHub Docs](https://docs.github.com/en/actions)

</details>






<details>
  <summary>Docker</summary>
  
# Docker
your-dockerhub-username == namespace

### 1) Make a `Dockerfile` with example contents as follows:
```Dockerfile
FROM node:20

# specify where whole project will install inside /usr/src
WORKDIR /usr/src/name_of_app 

COPY . .

RUN npm install

# change to where your server.js/index.js/app.js
WORKDIR /usr/src/name_of_app/src

EXPOSE 3000

CMD ["node", "server.js"]
```
### 2) Make a `.dockerignore` file with example contents as follows:
```.dockerignore
Dockerfile

.gitignore
node_modules
.env 

devlogs.txt
```
### 3) Make a `docker-compose.yml` file with example contents as follows:
- this file contains where to locate for environment variables while local development.
```YML
version: '3.8'

services:
  app:
    image: namespace/image_name
    build: .
    ports:
      - '3000:3000'
    env_file:
      - .env
```
### 4) Build an image:
- `docker build . -t namespace/image_name` ==> run this command where you have your docker files
### 5) Push image to DockerHub:
- `docker push namespace/image_name`
### 6) Pull images from DockerHub:
- `docker pull namespace/image_name`

---
### Run an image locally *(without env variables)*:
- You typically specify the image (`app`) and additional flags (e.g., `-p` for port mapping, `-v` for volumes).
- Example: `docker run -p 3000:3000 app`.
- Above examples tells that port 3000 of machine is mapped to port 3000 of container, so `docker run -p machine_port:container_port image_name`.
### Run an image locally *(with env variables)*:
`docker run --env-file ./path/to/.env -p 3000:3000 namespace/image_name:latest`
</details>


