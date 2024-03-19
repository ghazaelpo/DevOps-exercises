# Docker

# 01 - Pull Docker Image

## Draw by your self a representation of the docker Architecture

![Brainwriting.jpg](Docker%20b88721d15819492caf18201a5de72056/Brainwriting.jpg)

The architecture is very simple, Docker has three main blocks; Client, Host and Registry. We are the client and use a CLI to work with docker, through this tool we can execute commands and send them to the Docker Engine or Daemon, this one interpret our instructions and then take actions to build or run a specific image and finally create a container. Also we have a registry to save our images, this registry is Docker Hub, it is a tool to manage and share our images. Docker infrastructure allow us have containers, build images, manage Dockerfiles and all this through the first block, the client. 

## Explain the importance of Docker Hub into the Docker Architecture

The architecture is mainly based in image files, Docker has to manage these files and we working them. Docker Hub is a service allow us manage and share our images so this way we can work with another ones and use a safe space to save images written by us. In this tool we can find a thousand of images from different technology suppliers for use and apply them in our projects. We can find Python, Java, Apache images to run our projects as a lightly way.

**Docker Hub is very important because:**

> It is the world’s largest repository of container images with an array of content sources including container community developers, open source projects and independent software vendors (ISV) building and distributing their code in containers.
> 

## Provide an alternative solution to the use of Docker Hub

There is no one size fits all solution. But in this case if I have to choose a registry other than Docker I would like GitHub Container Registry. Let me explain my choice in the next question.

## Compare and analyze Docker Hub VS your alternative solution and identify the pros and cons

- Docker Hub vs GitHub Container Registry

GitHub is a very popular platform and recently has more services to offer than years ago. GitHub Container Registry, a new GitHub service for publishing and managing Docker images and OCI (Open Container Initiative) images within GitHub, is now generally available. This service belong to the new GitHub platform: GitHub Packages. 

GitHub Packages is a platform for hosting and managing packages, including containers and other dependencies. GitHub Packages combines your source code and packages in one place to provide integrated permissions management and billing, **so you can centralize your software development on GitHub.**

GitHub container has similar characteristics to Docker Hub but the main difference is the mentioned above: **Centralize your software Development on GitHub.** 

- You can have as many different tools in the same place and manage your changes, files, dependencies, containers with you whole entire team.
- It is relatively cheaper than Docker and other solutions.
- By the way, GitHub Container Registry provides public repositories. However, anyone who wants to download your container image needs to authenticate with a GitHub user account. Docker Hub allows unauthenticated access as well.
- There are not restrictions for public repositories as in Docker Hub. It introduced strict rate limits for repositories on a free plan.
    - 100 pulls for unauthenticated users per 6 hours.
    - 200 pulls for authenticated users per 6 hours.
    

Choose the platform based on your needs for a specific scenario. There are some characteristics from the platforms fit in your requirements. Even you can use more than one container registry but the efficiently is try to create an entire Software Development environment. GitHub is very popular, easy how-know and cheaper than other platforms.

## Mention the docker commands involved to Docker Hub

```docker
# Create your Repo on Docker Hub
docker push ghazaelpo/my-private-repo
# Get your repo to your local machine
docker pull ghazaelpo/my-private-repo:latest
# Build your repo
docker build -t ghazaelpo/my-private-repo
#Execute your repo
docker run ghazaelpo/my-private-repo
```