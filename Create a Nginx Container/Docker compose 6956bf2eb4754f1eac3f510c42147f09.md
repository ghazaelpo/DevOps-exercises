# Docker compose

Use Docker compose to start python Flask app and Nginx at same time.

### Instructions

1. Create a new file named ***flask-example.py***

```bash
genaroparedes@GenaroParedes-MacBook-Pro 05-Docker_compose % vim flask-example-py 
genaroparedes@GenaroParedes-MacBook-Pro 05-Docker_compose % cat flask-example-py 
from flask import Flask

    app = Flask(__name__)

    @app.route("/")
    def hello():
        return "Hello World!"

    if __name__ == "__main__":
        app.run('0.0.0.0')
```

1. Create a new file named Dockerfile

```bash
genaroparedes@GenaroParedes-MacBook-Pro 05-Docker_compose % vim Dockerfile 
genaroparedes@GenaroParedes-MacBook-Pro 05-Docker_compose % cat Dockerfile 
FROM python:3

WORKDIR /usr/src/app

RUN pip install Flask

COPY . .

CMD [ "python", "./flask-example.py" ]
```

1. Create a new file named docker-compose.yml

```bash
genaroparedes@GenaroParedes-MacBook-Pro 05-Docker_compose % vim docker-compose.yml 
genaroparedes@GenaroParedes-MacBook-Pro 05-Docker_compose % cat docker-compose.yml 
version: '3'
ervices:
  flask-example:
    restart: always
    build:
      dockerfile: Dockerfile
      context: .
     ports:
       - '81:5000'
     web:
       image: nginx
       ports:
         - '80:80'
```

1. Run the below command in order to create/build and run images

```bash
genaroparedes@GenaroParedes-MacBook-Pro 05-Docker_compose % docker-compose up --build -d
[+] Running 7/7
 ⠿ web Pulled                                                                          11.0s
   ⠿ a330b6cecb98 Pull complete                                                         7.7s
   ⠿ e0ad2c0621bc Pull complete                                                         9.0s
   ⠿ 9e56c3e0e6b7 Pull complete                                                         9.1s
   ⠿ 09f31c94adc6 Pull complete                                                         9.1s
   ⠿ 32b26e9cdb83 Pull complete                                                         9.2s
   ⠿ 20ab512bbb07 Pull complete                                                         9.3s
[+] Building 6.8s (10/10) FINISHED                                                           
 => [internal] load build definition from Dockerfile                                    0.0s
 => => transferring dockerfile: 147B                                                    0.0s
 => [internal] load .dockerignore                                                       0.0s
 => => transferring context: 2B                                                         0.0s
 => [internal] load metadata for docker.io/library/python:3                             1.1s
 => [auth] library/python:pull token for registry-1.docker.io                           0.0s
 => [1/4] FROM docker.io/library/python:3@sha256:e6654afa815122b13242fc9ff513e2d14b005  0.0s
 => [internal] load build context                                                       0.0s
 => => transferring context: 672B                                                       0.0s
 => CACHED [2/4] WORKDIR /usr/src/app                                                   0.0s
 => [3/4] RUN pip install Flask                                                         4.8s
 => [4/4] COPY . .                                                                      0.0s
 => exporting to image                                                                  0.6s
 => => exporting layers                                                                 0.6s
 => => writing image sha256:1298789a8946b7673a2ad9c0f309ec2f263a41ec31efa2217ff45ddd4a  0.0s 
 => => naming to docker.io/library/docker_compose_flask-example                         0.0s 
                                                                                             
Use 'docker scan' to run Snyk tests against images to find vulnerabilities and learn how to fix them
[+] Running 3/3
 ⠿ Network docker_compose_default            Create...                                  0.1s
 ⠿ Container docker_compose_flask-example_1  Started                                    0.8s
 ⠿ Container docker_compose_web_1            Starte...                                  0.8s
```

1. Display Images

```bash
genaroparedes@GenaroParedes-MacBook-Pro 05-Docker_compose % docker-compose images
Container                        Repository                     Tag                 Image Id            Size
docker_compose_flask-example_1   docker_compose_flask-example   latest              1298789a8946        922MB
docker_compose_web_1             nginx                          latest              ad4c705f24d3        133MB
```

1. Display current running containers

```bash
genaroparedes@GenaroParedes-MacBook-Pro 05-Docker_compose % docker ps -a
CONTAINER ID   IMAGE                          COMMAND                  CREATED              STATUS              PORTS                                   NAMES
0f3c777fa85d   docker_compose_flask-example   "python ./flask-exam…"   About a minute ago   Up About a minute   0.0.0.0:81->5000/tcp, :::81->5000/tcp   docker_compose_flask-example_1
9cf676e1afdc   nginx                          "/docker-entrypoint.…"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, :::80->80/tcp       docker_compose_web_1
genaroparedes@GenaroParedes-MacBook-Pro 05-Docker_compose % docker-compose ps
NAME                             COMMAND                  SERVICE             STATUS              PORTS
docker_compose_flask-example_1   "python ./flask-exam…"   flask-example       running             0.0.0.0:81->5000/tcp, :::81->5000/tcp
docker_compose_web_1             "/docker-entrypoint.…"   web                 running             0.0.0.0:80->80/tcp, :::80->80/tcp
```

- What are the benefits to use docker compose?

You can define all your services, volumes, exposed ports and even multi-containers, it is very powerful and all these in just one file, it is very important mention you can build using this file in one command as the previous exercise.

- Explain the docker compose file and the commands/directives used in this example

```bash
genaroparedes@GenaroParedes-MacBook-Pro 05-Docker_compose % cat docker-compose.yml 
#Define the docker-compose version, 3 is the recommended 
version: '3'
#Services defined by us, in our case the flask example and the service web...
#Provide by nginx
#We have define our exposed ports as well and the  
services:
  flask-example: #flask image provide by our dockerfile
    restart: always
    build:
      dockerfile: Dockerfile
      context: .
     ports:
       - '81:5000'
     web: #nginx image provide for docker hub
       image: nginx
       ports:
         - '80:80'
```

- Investigate and explain what is the use of --scale option

This command allow you run more than one instances for your services and exposed it using different ports so as this way we can create multiple services on different containers and exposed them.