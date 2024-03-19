# Lab 2, the microservice approach, DockerCompose

### Instructions

For this lab, you will migrate your stack of services from Lab01 to docker images using docker compose, and expose to the outside only the reverse proxy (nginx).

1. [Follow the steps on this tutorial to deploy a Ghost Blog using docker compose.](https://www.linode.com/docs/websites/cms/ghost/how-to-install-ghost-cms-with-docker-compose-on-ubuntu-18-04/)
    - NOTE: You can skip the third step in the **"Before You Begin"** section and use the same domain from the previous lab.
    

I will use this domain [lab02.centralus.cloudapp.azure.com](http://lab02.centralus.cloudapp.azure.com)

I have already installed Docker and Docker compose. 

To proceed with all necessary packages installation first we must ensure our system is up to date:

```bash
sudo apt update && sudo apt upgrade
```

After the update we need to get a certificate to our web. Use [Certbot](https://certbot.eff.org/) to request and download a free certificate from [Let’s Encrypt](https://letsencrypt.org/): 

![Screen Shot 2021-10-25 at 16.56.42.png](Lab%202,%20the%20microservice%20approach,%20DockerCompose%200e8cad5f9d7444eb8dafa651cbf1a366/Screen_Shot_2021-10-25_at_16.56.42.png)

![Screen Shot 2021-10-25 at 16.58.53.png](Lab%202,%20the%20microservice%20approach,%20DockerCompose%200e8cad5f9d7444eb8dafa651cbf1a366/Screen_Shot_2021-10-25_at_16.58.53.png)

Generate the certificate as per below:

```bash
sudo certbot certonly --standalone -d lab02.centralus.cloudapp.azure.com
```

![Screen Shot 2021-10-25 at 17.00.11.png](Lab%202,%20the%20microservice%20approach,%20DockerCompose%200e8cad5f9d7444eb8dafa651cbf1a366/Screen_Shot_2021-10-25_at_17.00.11.png)

The purpose of this exercise is install all the required packages using Docker compose, in this case:

- The Ghost service itself
- A database (MySQL) that will store our blog posts
- A web server (NGINX) that will proxy requests on HTTP and HTTPS to your Ghost service

These services are listed in a single Docker Compose file.

We are going to work using a new user different from default:

![Screen Shot 2021-10-25 at 17.10.28.png](Lab%202,%20the%20microservice%20approach,%20DockerCompose%200e8cad5f9d7444eb8dafa651cbf1a366/Screen_Shot_2021-10-25_at_17.10.28.png)

To achieve the mentioned above is necessary create a Docker compose file, so create and change to a directory to hold our new Docker Compose services:

```bash
test02@lab02:~$ mkdir ghost && cd ghost
```

After the Ghost directory creation we will define our Docker compose file inside it:

![Screen Shot 2021-10-25 at 17.15.24.png](Lab%202,%20the%20microservice%20approach,%20DockerCompose%200e8cad5f9d7444eb8dafa651cbf1a366/Screen_Shot_2021-10-25_at_17.15.24.png)

And then create the following directories as per the tutorial requirements:

![Screen Shot 2021-10-25 at 17.17.21.png](Lab%202,%20the%20microservice%20approach,%20DockerCompose%200e8cad5f9d7444eb8dafa651cbf1a366/Screen_Shot_2021-10-25_at_17.17.21.png)

The Docker Compose file relies on a customized NGINX image. This image will be packaged with the appropriate server block settings.

We will create a new `nginx` directory for this image in the `ghost` directory:

![Screen Shot 2021-10-25 at 17.19.27.png](Lab%202,%20the%20microservice%20approach,%20DockerCompose%200e8cad5f9d7444eb8dafa651cbf1a366/Screen_Shot_2021-10-25_at_17.19.27.png)

In the same nginx folder we will create default.conf file, this configuration will redirect all requests on HTTP to HTTPS (except for Let’s Encrypt challenge requests), and all requests on HTTPS will be proxied to the Ghost service.

![Screen Shot 2021-10-25 at 17.21.29.png](Lab%202,%20the%20microservice%20approach,%20DockerCompose%200e8cad5f9d7444eb8dafa651cbf1a366/Screen_Shot_2021-10-25_at_17.21.29.png)

After the certificate creation, have defined the docker compose file and the nginx image we can proceed to build our docker compose file:

![Screen Shot 2021-10-25 at 17.24.33.png](Lab%202,%20the%20microservice%20approach,%20DockerCompose%200e8cad5f9d7444eb8dafa651cbf1a366/Screen_Shot_2021-10-25_at_17.24.33.png)

**Application available via web browser**

![Screen Shot 2021-10-25 at 17.25.27.png](Lab%202,%20the%20microservice%20approach,%20DockerCompose%200e8cad5f9d7444eb8dafa651cbf1a366/Screen_Shot_2021-10-25_at_17.25.27.png)

**Connection is secure**

![Screen Shot 2021-10-25 at 17.26.33.png](Lab%202,%20the%20microservice%20approach,%20DockerCompose%200e8cad5f9d7444eb8dafa651cbf1a366/Screen_Shot_2021-10-25_at_17.26.33.png)