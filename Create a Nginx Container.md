# Create a Nginx Container

*First I will give a quick answer for each question and at the bottom of this document I'm going to explain and apply all the concepts through an exercise.*

## Explain the importance of use tags for images

Use tags while you are pulling images is very important because this parameter allow you specify the image version you requires. For example if your project works with specific image version, you can pull it just typing as per the below format:

```docker
# general format 
docker pull name_image:version(x.xx)

# This example is nginx 1.15 version 
docker pull nginx:1.16
```

If you don't specify the version using the tag, this will the *latest.* I will explain it in the next question.

## What is the meaning of ***latest*** tag ?

*Latest* tag means the newest version for the image that you are pulling, as I mentioned above, if you don't specify the version for your image, you will get the latest version of that image

## Explain how to remove an specific image version

If you want to remove an specific image version just type the below command:

```python
docker rmi Image_ID
```

## Create a sequence of commands to remove all the images except latest (Using Bash or patterns or any other solution)

```docker
docker rmi -f $(docker images | grep -v "Image_ID" | awk 'NR>1{print$3}')
```

# **In this part I will create a NGINX container, explain and apply all the previous questions to give more color about it.**

- **Pulling images**

```docker
# The first step is pull the required image.
# In our case will nginx 

# I will pull three different versions for clarify the use of tag

# Without tag just using the general format docker pull name_image
genaroparedes@GenaroParedes-MacBook-Pro exercises % docker pull nginx
# As you can see in this part is pulling the newest version because...
# We did not specify the version so the tag is LATEST
Using default tag: latest
latest: Pulling from library/nginx
a330b6cecb98: Already exists 
e0ad2c0621bc: Already exists 
9e56c3e0e6b7: Already exists 
09f31c94adc6: Already exists 
32b26e9cdb83: Already exists 
20ab512bbb07: Already exists 
Digest: sha256:853b221d3341add7aaadf5f81dd088ea943ab9c918766e295321294b035f3f3e
Status: Downloaded newer image for nginx:latest
docker.io/library/nginx:latest

# Pulling version 1.16 
genaroparedes@GenaroParedes-MacBook-Pro exercises % docker pull nginx:1.16
1.16: Pulling from library/nginx
54fec2fa59d0: Already exists 
5546cfc92772: Already exists 
50f62e3cdaf7: Already exists 
Digest: sha256:d20aa6d1cae56fd17cd458f4807e0de462caf2336f0b70b5eeb69fcaaf30dd9c
Status: Downloaded newer image for nginx:1.16
docker.io/library/nginx:1.16
```

- **Creating/running a container**

```docker
# List the existing docker containers running in your docker host...
# no Nginx containers are running:
genaroparedes@GenaroParedes-MacBook-Pro exercises % docker ps 
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

# Create/run a container for the latest version of Nginx image.
genaroparedes@GenaroParedes-MacBook-Pro exercises % docker run -d  nginx                                         
5af07e9959c7decf27c6d1a6d803bb81bd62044c133b68fb7e257b7667ca9fca

# Create/run a container for the 1.16 version of Nginx image.
genaroparedes@GenaroParedes-MacBook-Pro exercises % docker run -d nginx:1.16
d6655dab6f1e9fc35483230ed64db17d121d42b6b2b63cef2e53500607d1a676

# List the existing docker containers running in your docker host...
# you should see two containers running one for latest and one more...
# for 1.16 versions
genaroparedes@GenaroParedes-MacBook-Pro exercises % docker ps 
CONTAINER ID   IMAGE        COMMAND                  CREATED              STATUS              PORTS     NAMES
d6655dab6f1e   nginx:1.16   "nginx -g 'daemon of…"   About a minute ago   Up About a minute   80/tcp    sleepy_lovelace
5af07e9959c7   nginx        "/docker-entrypoint.…"   2 minutes ago        Up 2 minutes        80/tcp    gifted_bouman

# Create a Docker container from Nginx version 1.15 which...
# is not downloaded to your local images...
# and additionally assign a custom name:
		# Make sure Nginx 1.15 is not in your local images
		CONTAINER ID   IMAGE        COMMAND                  CREATED         STATUS         PORTS     NAMES
d6655dab6f1e   nginx:1.16   "nginx -g 'daemon of…"   4 minutes ago   Up 4 minutes   80/tcp    sleepy_lovelace
5af07e9959c7   nginx        "/docker-entrypoint.…"   5 minutes ago   Up 5 minutes   80/tcp    gifted_bouman
		# Create docker container for Nginx 1.15 which is not...
		# present in your local images repository.
		genaroparedes@GenaroParedes-MacBook-Pro exercises % docker run -d --name my-custom-name nginx:1.15 
Unable to find image 'nginx:1.15' locally
1.15: Pulling from library/nginx
743f2d6c1f65: Already exists 
6bfc4ec4420a: Already exists 
688a776db95f: Already exists 
Digest: sha256:23b4dcdf0d34d4a129755fc6f52e1c6e23bb34ea011b315d87e193033bcd1b68
Status: Downloaded newer image for nginx:1.15
4c8a070b8072ea8f0f70f19e47c90fa34269793747cfdfec68a44f9cb9df6769

# List the running containers and note the changes for ***Name*** and ***TAG***
genaroparedes@GenaroParedes-MacBook-Pro exercises % docker ps
CONTAINER ID   IMAGE        COMMAND                  CREATED          STATUS          PORTS     NAMES
4c8a070b8072   nginx:1.15   "nginx -g 'daemon of…"   40 seconds ago   Up 39 seconds   80/tcp    my-custom-name
d6655dab6f1e   nginx:1.16   "nginx -g 'daemon of…"   8 minutes ago    Up 8 minutes    80/tcp    sleepy_lovelace
5af07e9959c7   nginx        "/docker-entrypoint.…"   9 minutes ago    Up 9 minutes    80/tcp    gifted_bouman
```

- **I will delete all created images except the latest version**

```docker
# It is mandatory stop the containers to be able to delete the images...
# that you want
genaroparedes@GenaroParedes-MacBook-Pro exercises % docker stop $(docker ps | awk 'NR>1{print$1}')
4c8a070b8072
d6655dab6f1e
5af07e9959c7
genaroparedes@GenaroParedes-MacBook-Pro exercises % docker ps 
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

# Then just created a similar code line as above but switch docker stop..
# to docker rmi -f and add a pipeline using grep -v for except the id image
genaroparedes@GenaroParedes-MacBook-Pro exercises % docker rmi -f $(docker images | grep -v "ad4c705f24d3" | awk 'NR>1{print$3}')
Untagged: nginx:1.16
Untagged: nginx@sha256:d20aa6d1cae56fd17cd458f4807e0de462caf2336f0b70b5eeb69fcaaf30dd9c
Deleted: sha256:dfcfd8e9a5d38fb82bc8f9c299beba2df2232b7712b62875d5238cead7a5831c
Untagged: nginx:1.15
Untagged: nginx@sha256:23b4dcdf0d34d4a129755fc6f52e1c6e23bb34ea011b315d87e193033bcd1b68
Deleted: sha256:53f3fd8007f76bd23bf663ad5f5009c8941f63828ae458cef584b5f85dc0a7bf
```

[Dockerfile ](Create%20a%20Nginx%20Container%203b996eee9ebd4ced8c502e86d8c1874b/Dockerfile%20e865332acb734ad0a9b5381f3b65843d.md)

[Dockerfile ll](Create%20a%20Nginx%20Container%203b996eee9ebd4ced8c502e86d8c1874b/Dockerfile%20ll%208d2503778f754dfdbc5f44ac0bba103a.md)

[Docker compose](Create%20a%20Nginx%20Container%203b996eee9ebd4ced8c502e86d8c1874b/Docker%20compose%206956bf2eb4754f1eac3f510c42147f09.md)

[Build tf+aws image and upload to docker hub](Create%20a%20Nginx%20Container%203b996eee9ebd4ced8c502e86d8c1874b/Build%20tf+aws%20image%20and%20upload%20to%20docker%20hub%20784265cf9b4244f0a629e7475308017b.md)

[Build tf+azure image and upload to docker hub](Create%20a%20Nginx%20Container%203b996eee9ebd4ced8c502e86d8c1874b/Build%20tf+azure%20image%20and%20upload%20to%20docker%20hub%20e3f061cfd4854b6284f46012894bce4f.md)

[Cloud provider services](Create%20a%20Nginx%20Container%203b996eee9ebd4ced8c502e86d8c1874b/Cloud%20provider%20services%20ec95fa8ddfe14986a52ba87a3558b532.md)