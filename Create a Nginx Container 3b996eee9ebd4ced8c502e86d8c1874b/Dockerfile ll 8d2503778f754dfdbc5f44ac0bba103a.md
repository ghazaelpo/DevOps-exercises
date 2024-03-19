# Dockerfile ll

# Create and run a basic python container and run a test python script.

### Instructions

Create a custom docker image using Dockerfile and manually install nodejs and any remaining dependency to run the following project [https://github.com/geerlingguy/demo-nodejs-api](https://github.com/geerlingguy/demo-nodejs-api)

You can test if this app is running by browsing to the `/hello/MY_NAME` resource.

### Steps:

- Git clone the given repository to our work directory

```bash
git clone [https://github.com/geerlingguy/demo-nodejs-api](https://github.com/geerlingguy/demo-nodejs-api)
```

## INSTALLING NODEJS, MOVING THE APP TO THE IMAGE AND EXPOSING PORTS

- Create the required custom docker image using Dockerfile, please refer to the comments to understand every part of this file

```bash
genaroparedes@GenaroParedes-MacBook-Pro demo-nodejs-api % vim Dockerfile
#Install node 14 version
FROM node:14

#Create your work directory, all will save here
WORKDIR /usr/src/app

#Get all package json for npm works
COPY package*.json ./

#Install npm for your code works
RUN npm install

#Copy all your files from your current path to the container...
#as this way you can execute all the dependencies in the container...
#without failed
COPY . .

#Expose 8080 port to access through 
EXPOSE 8080

#Execute js app
CMD ["node", "app.js"]
```

- Build our images as per below

```bash
genaroparedes@GenaroParedes-MacBook-Pro demo-nodejs-api % docker build -t nodejs-test-genaro .                     
[+] Building 1.5s (11/11) FINISHED                                                                                                                          
 => [internal] load build definition from Dockerfile                                                                                                   0.0s
 => => transferring dockerfile: 414B                                                                                                                   0.0s
 => [internal] load .dockerignore                                                                                                                      0.0s
 => => transferring context: 2B                                                                                                                        0.0s
 => [internal] load metadata for docker.io/library/node:14                                                                                             1.2s
 => [auth] library/node:pull token for registry-1.docker.io                                                                                            0.0s
 => [internal] load build context                                                                                                                      0.0s
 => => transferring context: 3.39kB                                                                                                                    0.0s
 => [1/5] FROM docker.io/library/node:14@sha256:4164d987bfceb62b17db4938d535dd31fc50d6ee0b4e00ac7a774f82af408d48                                       0.0s
 => CACHED [2/5] WORKDIR /usr/src/app                                                                                                                  0.0s
 => CACHED [3/5] COPY package*.json ./                                                                                                                 0.0s
 => CACHED [4/5] RUN npm install                                                                                                                       0.0s
 => [5/5] COPY . .                                                                                                                                     0.0s
 => exporting to image                                                                                                                                 0.1s
 => => exporting layers                                                                                                                                0.0s
 => => writing image sha256:2f0e7cab44dc30b90e1b906806cd001a8255508010cc4582d046adc9deed5283                                                           0.0s
 => => naming to docker.io/library/nodejs-test-genaro                                                                                                  0.0s

Use 'docker scan' to run Snyk tests against images to find vulnerabilities and learn how to fix them
```

- Create our container and set the expose port to access and test if this app is running by browsing to the `/hello/MY_NAME` resource.

```bash
genaroparedes@GenaroParedes-MacBook-Pro demo-nodejs-api % docker run -d -p 8080:8080 --name Genaro_test nodejs-test-genaro 
53919e0c023bcb9b6ba5b1cc2b51e44a6e32fef929cfbeb8403b8814c8480be5
```

## APP RUNNING

![Screen Shot 2021-09-26 at 15.35.14.png](Dockerfile%20ll%208d2503778f754dfdbc5f44ac0bba103a/Screen_Shot_2021-09-26_at_15.35.14.png)