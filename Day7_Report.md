1. What is Dockerfile?

A Dockerfile is a text file that contains instructions used by Docker to build a custom Docker image. It defines the base image, application files, configuration, ports, and commands required to run an application inside a container.

Example:

FROM nginx:latest
COPY index.html /usr/share/nginx/html/
COPY styles.css /usr/share/nginx/html/
EXPOSE 80

2. Dockerfile Instructions

Important Dockerfile instructions practiced during Day 7:

Instruction

Purpose

FROM

Specifies the base image

COPY

Copies files from the build context into the image

RUN

Executes commands while building the image

WORKDIR

Sets the working directory

EXPOSE

Documents the port used by the application

CMD

Provides the default command for the container

ENTRYPOINT

Defines the main executable for the container

3. Docker Build Process

The Docker image was created from the Dockerfile using:

sudo docker build -t devops-website:v1 .

The build process is:

Dockerfile
     ↓
Docker Build Context
     ↓
Docker Build
     ↓
Docker Image
     ↓
Docker Container

To verify the image:

sudo docker images

4. Docker Image Versions

Docker image tags are used to identify different versions of an image.

Example:

devops-website:v1
devops-website:v2
devops-website:latest

Build a versioned image:

sudo docker build -t devops-website:v1 .

Run it:

sudo docker run -d --name devops-website-container -p 8080:80 devops-website:v1

Using tags makes it easier to manage and identify different application versions.

5. .dockerignore

The .dockerignore file specifies files and directories that should not be sent to Docker as part of the build context.

Example:

.git
.gitignore
README.md
*.log

Create the file:

touch .dockerignore

To display hidden files using tree:

tree -a

Example project structure:

.
├── .dockerignore
├── Dockerfile
├── index.html
└── styles.css

The .dockerignore file helps reduce unnecessary build context and keeps unwanted files out of the image build process.

6. Port Mapping

Docker containers can expose application ports to the host machine.

For the Nginx web server:

sudo docker run -d --name devops-website-container -p 8080:80 devops-website:v1

The mapping is:

Host Port 8080 → Container Port 80

The website can then be accessed through:

http://localhost:8080

7. Nginx Container

Nginx was used as the base image for the custom website image.

Dockerfile:

FROM nginx:latest

COPY index.html /usr/share/nginx/html/
COPY styles.css /usr/share/nginx/html/

EXPOSE 80

Build the image:

sudo docker build -t devops-website:v1 .

Run the container:

sudo docker run -d --name devops-website-container -p 8080:80 devops-website:v1

Check the running container:

sudo docker ps

8. Docker Hub

Docker Hub is a public registry used to store and share Docker images.

Typical workflow:

sudo docker login
sudo docker tag devops-website:v1 <dockerhub-username>/devops-website:v1
sudo docker push <dockerhub-username>/devops-website:v1

To download an image:

sudo docker pull <dockerhub-username>/devops-website:v1

Docker Hub makes it possible to share custom Docker images with other systems and team members.

9. Troubleshooting

The following Docker commands were used for troubleshooting:

sudo docker build -t devops-website:v1 .
sudo docker images
sudo docker ps
sudo docker ps -a
sudo docker logs devops-website-container
sudo docker inspect devops-website-container

Useful commands:

Check running containers

sudo docker ps

Check all containers

sudo docker ps -a

Check image list

sudo docker images

View container logs

sudo docker logs devops-website-container

Inspect a container

sudo docker inspect devops-website-container

10. Problems Faced

Problem 1 – Duplicate Dockerfile names

The project initially contained:

Dockerfile
dockerfile

Linux treats uppercase and lowercase filenames as different files.

Problem 2 – Incorrect Dockerfile configuration

Incorrect base image, COPY paths, commands, or port configuration can cause Docker build or container startup failures.

Problem 3 – Container name conflict

If a container with the same name already exists, Docker reports a name conflict.

Problem 4 – Port mapping issues

Incorrect host-to-container port mapping can prevent access to the website.

Problem 5 – Hidden .dockerignore file

.dockerignore starts with a dot, so it is hidden in normal directory listings.

11. Solutions

Solution 1 – Remove duplicate Dockerfile

Keep the correctly named file:

rm dockerfile

Verify:

tree -a

Solution 2 – Verify Dockerfile

cat Dockerfile

Check the FROM, COPY, and EXPOSE instructions.

Solution 3 – Check existing containers

sudo docker ps -a

Remove an unwanted container:

sudo docker rm devops-website-container

Then run the container again.

Solution 4 – Verify port mapping

sudo docker ps

Check that the container has a mapping similar to:

0.0.0.0:8080->80/tcp

Solution 5 – Display hidden files

tree -a

12. Screenshots

Add screenshots from the Day 7 practical work below.

Screenshot 1 – Project Structure

Add screenshot showing:

tree -a

Expected structure:

.
├── .dockerignore
├── Dockerfile
├── index.html
└── styles.css

Screenshot 2 – Dockerfile

Add screenshot showing:

cat Dockerfile

Screenshot 3 – Docker Image

Add screenshot showing:

sudo docker images

Screenshot 4 – Running Container

Add screenshot showing:

sudo docker ps

Screenshot 5 – Website

Add a browser screenshot showing:

http://localhost:8080

Screenshot 6 – Docker Troubleshooting

Add screenshots of relevant commands such as:

sudo docker logs devops-website-container
sudo docker inspect devops-website-container

13. What I Learned

During Day 7, I learned how to create and use a Dockerfile to build a custom Docker image. I practiced Dockerfile instructions such as FROM, COPY, and EXPOSE.

I learned how to build versioned Docker images using image tags such as v1. I also learned the purpose of .dockerignore and how to display hidden files using tree -a.

I practiced running an Nginx container and mapping the container's port 80 to host port 8080. I also learned how to inspect containers, view logs, check images, and troubleshoot common Docker problems.

Finally, I learned the basic workflow for tagging and pushing custom Docker images to Docker Hub.

Day 7 Summary

The complete workflow practiced was:

Create Website
      ↓
Create Dockerfile
      ↓
Create .dockerignore
      ↓
Build Custom Image
      ↓
Tag Image Version
      ↓
Run Nginx Container
      ↓
Map Port 8080 → 80
      ↓
Test Website
      ↓
Troubleshoot
      ↓
Tag for Docker Hub
      ↓
Push Image

Status: Day 7 Dockerfile & Custom Docker Image task completed.
