# Azure DevOps Introduction

## Create a New Azure DevOps Organization

Click on Azure DevOps icon and then click on New organization

![Screen Shot 2021-10-12 at 11.50.38.png](Azure%20DevOps%20Introduction%20e683d2acccc547dfb9873b3f96d47869/Screen_Shot_2021-10-12_at_11.50.38.png)

Choose a name and the location for your new organization

![Screen Shot 2021-10-12 at 11.53.14.png](Azure%20DevOps%20Introduction%20e683d2acccc547dfb9873b3f96d47869/Screen_Shot_2021-10-12_at_11.53.14.png)

## Create a New Azure DevOps Project and name it whatever you like and mark it as public

![Screen Shot 2021-10-12 at 11.55.06.png](Azure%20DevOps%20Introduction%20e683d2acccc547dfb9873b3f96d47869/Screen_Shot_2021-10-12_at_11.55.06.png)

Project created 

![Screen Shot 2021-10-12 at 11.55.41.png](Azure%20DevOps%20Introduction%20e683d2acccc547dfb9873b3f96d47869/Screen_Shot_2021-10-12_at_11.55.41.png)

## Fork, Import or Push a sample App inside the Repos Section of the newly created Project

Go to Repos section, click on import and then paste the GitHub URL

![Screen Shot 2021-10-12 at 13.25.20.png](Azure%20DevOps%20Introduction%20e683d2acccc547dfb9873b3f96d47869/Screen_Shot_2021-10-12_at_13.25.20.png)

Wait until the App complete the importing process

![Screen Shot 2021-10-12 at 13.26.50.png](Azure%20DevOps%20Introduction%20e683d2acccc547dfb9873b3f96d47869/Screen_Shot_2021-10-12_at_13.26.50.png)

![Screen Shot 2021-10-12 at 13.27.01.png](Azure%20DevOps%20Introduction%20e683d2acccc547dfb9873b3f96d47869/Screen_Shot_2021-10-12_at_13.27.01.png)

![Screen Shot 2021-10-12 at 13.31.58.png](Azure%20DevOps%20Introduction%20e683d2acccc547dfb9873b3f96d47869/Screen_Shot_2021-10-12_at_13.31.58.png)

## Setup a simple build pipeline with both classic and Yaml pipelines that publishes an artifact called "drop"

Go to Pipelines sections and clink on Create Pipeline

![Screen Shot 2021-10-12 at 13.33.15.png](Azure%20DevOps%20Introduction%20e683d2acccc547dfb9873b3f96d47869/Screen_Shot_2021-10-12_at_13.33.15.png)

**To build a Classic Pipeline click on the below option** 

![Screen Shot 2021-10-12 at 13.39.51.png](Azure%20DevOps%20Introduction%20e683d2acccc547dfb9873b3f96d47869/Screen_Shot_2021-10-12_at_13.39.51.png)

After the classic editor selection we will see the below options, select Azure Repos Git to use our imported project and the default branch for us will be master

![Screen Shot 2021-10-12 at 13.41.05.png](Azure%20DevOps%20Introduction%20e683d2acccc547dfb9873b3f96d47869/Screen_Shot_2021-10-12_at_13.41.05.png)

Our project has a Dockerfile, we will build the artifact using an empty job

![Screen Shot 2021-10-12 at 13.48.03.png](Azure%20DevOps%20Introduction%20e683d2acccc547dfb9873b3f96d47869/Screen_Shot_2021-10-12_at_13.48.03.png)

Configure the agents and options to build our image

![Screen Shot 2021-10-12 at 14.03.00.png](Azure%20DevOps%20Introduction%20e683d2acccc547dfb9873b3f96d47869/Screen_Shot_2021-10-12_at_14.03.00.png)

Set automatic triggers to execute the pipeline once new code is available on the main branch

![Screen Shot 2021-10-12 at 14.08.36.png](Azure%20DevOps%20Introduction%20e683d2acccc547dfb9873b3f96d47869/Screen_Shot_2021-10-12_at_14.08.36.png)

After all the configuration run the pipeline 

![Screen Shot 2021-10-12 at 14.10.06.png](Azure%20DevOps%20Introduction%20e683d2acccc547dfb9873b3f96d47869/Screen_Shot_2021-10-12_at_14.10.06.png)

I ran the pipeline manually and automatically

![Screen Shot 2021-10-12 at 14.16.32.png](Azure%20DevOps%20Introduction%20e683d2acccc547dfb9873b3f96d47869/Screen_Shot_2021-10-12_at_14.16.32.png)

### Create the Pipeline using a YAML file

![Screen Shot 2021-10-12 at 14.27.59.png](Azure%20DevOps%20Introduction%20e683d2acccc547dfb9873b3f96d47869/Screen_Shot_2021-10-12_at_14.27.59.png)

![Screen Shot 2021-10-12 at 14.28.58.png](Azure%20DevOps%20Introduction%20e683d2acccc547dfb9873b3f96d47869/Screen_Shot_2021-10-12_at_14.28.58.png)

![Screen Shot 2021-10-12 at 14.29.49.png](Azure%20DevOps%20Introduction%20e683d2acccc547dfb9873b3f96d47869/Screen_Shot_2021-10-12_at_14.29.49.png)

![Screen Shot 2021-10-12 at 14.30.48.png](Azure%20DevOps%20Introduction%20e683d2acccc547dfb9873b3f96d47869/Screen_Shot_2021-10-12_at_14.30.48.png)

```bash
# Docker
# Build a Docker image
# https://docs.microsoft.com/azure/devops/pipelines/languages/docker

trigger:
- master

resources:
- repo: self

variables:
  tag: '$(Build.BuildId)'

stages:
- stage: Build
  displayName: Build image
  jobs:
  - job: Build
    displayName: Build
    pool:
      vmImage: ubuntu-latest
    steps:
    - task: Docker@2
      displayName: Build an image
      inputs:
        command: build
        dockerfile: '$(Build.SourcesDirectory)/app/Dockerfile'
        tags: |
          $(tag)
```

The Pipeline run again using the YML file

![Screen Shot 2021-10-12 at 14.34.54.png](Azure%20DevOps%20Introduction%20e683d2acccc547dfb9873b3f96d47869/Screen_Shot_2021-10-12_at_14.34.54.png)

Here is the yml file created

![Screen Shot 2021-10-12 at 14.35.40.png](Azure%20DevOps%20Introduction%20e683d2acccc547dfb9873b3f96d47869/Screen_Shot_2021-10-12_at_14.35.40.png)

## each time a new push to the main branch takes place, both pipelines should automatically run

![Screen Shot 2021-10-12 at 14.17.56.png](Azure%20DevOps%20Introduction%20e683d2acccc547dfb9873b3f96d47869/Screen_Shot_2021-10-12_at_14.17.56.png)

![Screen Shot 2021-10-12 at 14.18.16.png](Azure%20DevOps%20Introduction%20e683d2acccc547dfb9873b3f96d47869/Screen_Shot_2021-10-12_at_14.18.16.png)

## give access to the trainer and reviewers to the repos

![Screen Shot 2021-10-12 at 14.26.23.png](Azure%20DevOps%20Introduction%20e683d2acccc547dfb9873b3f96d47869/Screen_Shot_2021-10-12_at_14.26.23.png)