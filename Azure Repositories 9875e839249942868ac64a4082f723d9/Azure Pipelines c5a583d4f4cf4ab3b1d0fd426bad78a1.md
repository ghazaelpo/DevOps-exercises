# Azure Pipelines

**Activity 1**

Create a build YAML pipeline.

1. Get the sample application (fork): SpaceGame
    
    ![Screen Shot 2021-10-12 at 19.58.07.png](Azure%20Pipelines%20c5a583d4f4cf4ab3b1d0fd426bad78a1/Screen_Shot_2021-10-12_at_19.58.07.png)
    
    ![Screen Shot 2021-10-12 at 19.58.15.png](Azure%20Pipelines%20c5a583d4f4cf4ab3b1d0fd426bad78a1/Screen_Shot_2021-10-12_at_19.58.15.png)
    

1. Clone your fork locally.
    
    ![Screen Shot 2021-10-12 at 20.00.48.png](Azure%20Pipelines%20c5a583d4f4cf4ab3b1d0fd426bad78a1/Screen_Shot_2021-10-12_at_20.00.48.png)
    
    ![Screen Shot 2021-10-12 at 20.02.15.png](Azure%20Pipelines%20c5a583d4f4cf4ab3b1d0fd426bad78a1/Screen_Shot_2021-10-12_at_20.02.15.png)
    

1. Build and run the web app locally.

```bash
GenaroParedes-MacBook-Pro:mslearn-tailspin-spacegame-web genaroparedes$ dotnet build --configuration Release
Microsoft (R) Build Engine version 16.11.0+0538acc04 for .NET
Copyright (C) Microsoft Corporation. All rights reserved.

  Determining projects to restore...
  Restored /Users/genaroparedes/Documents/devops/AzureDevOps/mslearn-tailspin-spacegame-web/Tailspin.SpaceGame.Web/Tailspin.SpaceGame.Web.csproj (in 80 ms).
  Tailspin.SpaceGame.Web -> /Users/genaroparedes/Documents/devops/AzureDevOps/mslearn-tailspin-spacegame-web/Tailspin.SpaceGame.Web/bin/Release/net5.0/Tailspin.SpaceGame.Web.dll
  Tailspin.SpaceGame.Web -> /Users/genaroparedes/Documents/devops/AzureDevOps/mslearn-tailspin-spacegame-web/Tailspin.SpaceGame.Web/bin/Release/net5.0/Tailspin.SpaceGame.Web.Views.dll

Build succeeded.
    0 Warning(s)
    0 Error(s)

Time Elapsed 00:00:05.62
GenaroParedes-MacBook-Pro:mslearn-tailspin-spacegame-web genaroparedes$ dotnet run --configuration Release --no-build --project Tailspin.SpaceGame.Web
Hosting environment: Production
Content root path: /Users/genaroparedes/Documents/devops/AzureDevOps/mslearn-tailspin-spacegame-web/Tailspin.SpaceGame.Web
Now listening on: http://localhost:5000
Now listening on: https://localhost:5001
Application started. Press Ctrl+C to shut down.
```

![Screen Shot 2021-10-12 at 20.22.22.png](Azure%20Pipelines%20c5a583d4f4cf4ab3b1d0fd426bad78a1/Screen_Shot_2021-10-12_at_20.22.22.png)

1. Create the pipeline.
    1. In Azure DevOps, go to your project.
    2. Either from the project page or from the left pane, select Pipelines.
    3. Select Create Pipeline. On the **Connect** tab, select **GitHub**.
    4. On the **Connect** tab, select **GitHub**.
        
        When prompted, enter your GitHub credentials.
        
    5. On the Select tab, select your mslearn-tailspin-spacegame-web repository.
    6. To install the Azure Pipelines app, you might be redirected to GitHub. If so, scroll to the bottom, and select Approve and install.
    7. On the Configure tab, select ASP.NET Core. 
        
        ![Screen Shot 2021-10-12 at 20.57.54.png](Azure%20Pipelines%20c5a583d4f4cf4ab3b1d0fd426bad78a1/Screen_Shot_2021-10-12_at_20.57.54.png)
        
        On the Review tab, note the initial build configuration.
        
        ![Screen Shot 2021-10-12 at 21.08.00.png](Azure%20Pipelines%20c5a583d4f4cf4ab3b1d0fd426bad78a1/Screen_Shot_2021-10-12_at_21.08.00.png)
        
        This is a very basic configuration that Azure DevOps provides for you based on your app type, ASP.NET Core.
        
        On the Review tab, select Save and run. Next, to commit your changes to GitHub and start the build, select Save and run a second time.
        
    
    **Pipeline Running**
    
    ![Screen Shot 2021-10-12 at 21.10.51.png](Azure%20Pipelines%20c5a583d4f4cf4ab3b1d0fd426bad78a1/Screen_Shot_2021-10-12_at_21.10.51.png)
    
2. Add build task
    1. In Visual Studio Code, go to the integrated terminal.
    2. To fetch the latest changes from GitHub and update your main branch, run this git pull command.
    
    ```bash
    GenaroParedes-MacBook-Pro:mslearn-tailspin-spacegame-web genaroparedes$ git pull origin main
    remote: Enumerating objects: 3, done.
    remote: Counting objects: 100% (1/1), done.
    remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 2
    Unpacking objects: 100% (3/3), 1.03 KiB | 150.00 KiB/s, done.
    From https://github.com/ghazaelpo/mslearn-tailspin-spacegame-web
     * branch            main       -> FETCH_HEAD
       f236243..b86f968  main       -> origin/main
    Updating f236243..b86f968
    Fast-forward
     azure-pipelines.yml | 34 ++++++++++++++++++++++++++++++++++
     1 file changed, 34 insertions(+)
     create mode 100644 azure-pipelines.yml
    ```
    
    You see from the output that Git fetches a file named azure-pipelines.yml. This is the starter pipeline configuration that Azure Pipelines created for you. When you set up the pipeline, Azure Pipelines adds this file to your GitHub repository.
    

To fetch the latest changes from GitHub and update your main branch, run this git pull command.

```bash
GenaroParedes-MacBook-Pro:mslearn-tailspin-spacegame-web genaroparedes$ git checkout -B build-pipeline
Switched to a new branch 'build-pipeline'
```

In Visual Studio Code, modify azure-pipelines.yml as you see here:

```bash
trigger:
- '*'

pool:
  vmImage: 'ubuntu-20.04'
  demands:
  - npm

variables:
  buildConfiguration: 'Release'

steps:
- task: UseDotNet@2
  displayName: 'Use .NET SDK 5.x'
  inputs:
    packageType: sdk
    version: '5.x'

- task: Npm@1
  displayName: 'Run npm install'
  inputs:
    verbose: false

- script: './node_modules/.bin/node-sass Tailspin.SpaceGame.Web/wwwroot --output Tailspin.SpaceGame.Web/wwwroot'
  displayName: 'Compile Sass assets'

- task: gulp@1
  displayName: 'Run gulp tasks'

- script: 'echo "$(Build.DefinitionName), $(Build.BuildId), $(Build.BuildNumber)" > buildinfo.txt'
  displayName: 'Write build info'
  workingDirectory: Tailspin.SpaceGame.Web/wwwroot

- task: DotNetCoreCLI@2
  displayName: 'Restore project dependencies'
  inputs:
    command: 'restore'
    projects: '**/*.csproj'

- task: DotNetCoreCLI@2
  displayName: 'Build the project - Release'
  inputs:
    command: 'build'
    arguments: '--no-restore --configuration Release'
    projects: '**/*.csproj'
```

From the integrated terminal, to add azure-pipelines.yml to the index, commit the change, and push the change up to GitHub, run the following Git commands. These steps are similar to steps you performed earlier.

```bash
GenaroParedes-MacBook-Pro:mslearn-tailspin-spacegame-web genaroparedes$ git add azure-pipelines.yml
GenaroParedes-MacBook-Pro:mslearn-tailspin-spacegame-web genaroparedes$ git commit -m "Add build tasks"
[build-pipeline 512322e] Add build tasks
 1 file changed, 50 insertions(+), 34 deletions(-)
 rewrite azure-pipelines.yml (65%)
GenaroParedes-MacBook-Pro:mslearn-tailspin-spacegame-web genaroparedes$ git push origin build-pipeline
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 839 bytes | 839.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/ghazaelpo/mslearn-tailspin-spacegame-web.git
   b86f968..512322e  build-pipeline -> build-pipeline
```

This time, you push the `build-pipeline` branch, not the `main` branch, to GitHub.

Pushing the branch to GitHub triggers the build process in Azure Pipelines.

In Azure Pipelines, go to your build. To do so, on the side of the page, select Pipelines, and then select your pipeline. You see your commit message and that the build is running using the code from the build-pipeline branch.

![Screen Shot 2021-10-12 at 21.22.50.png](Azure%20Pipelines%20c5a583d4f4cf4ab3b1d0fd426bad78a1/Screen_Shot_2021-10-12_at_21.22.50.png)

# Publish the result to the pipeline

In .NET, you can package your app as a .zip file. You can then use the built-in PublishBuildArtifacts@1 task to publish the .zip file to Azure Pipelines.

In Visual Studio Code, modify azure-pipelines.yml as you see here:

```bash
trigger:
- '*'

pool:
  vmImage: 'ubuntu-20.04'
  demands:
  - npm

steps:
- task: UseDotNet@2
  displayName: 'Use .NET SDK 5.x'
  inputs:
    version: '5.x'

- task: Npm@1
  displayName: 'Run npm install'
  inputs:
    verbose: false

- script: './node_modules/.bin/node-sass Tailspin.SpaceGame.Web/wwwroot --output Tailspin.SpaceGame.Web/wwwroot'
  displayName: 'Compile Sass assets'

- task: gulp@1
  displayName: 'Run gulp tasks'

- script: 'echo "$(Build.DefinitionName), $(Build.BuildId), $(Build.BuildNumber)" > buildinfo.txt'
  displayName: 'Write build info'
  workingDirectory: Tailspin.SpaceGame.Web/wwwroot

- task: DotNetCoreCLI@2
  displayName: 'Restore project dependencies'
  inputs:
    command: 'restore'
    projects: '**/*.csproj'

- task: DotNetCoreCLI@2
  displayName: 'Build the project - Release'
  inputs:
    command: 'build'
    arguments: '--no-restore --configuration Release'
    projects: '**/*.csproj'

- task: DotNetCoreCLI@2
  displayName: 'Publish the project - Release'
  inputs:
    command: 'publish'
    projects: '**/*.csproj'
    publishWebProjects: false
    arguments: '--no-build --configuration Release --output $(Build.ArtifactStagingDirectory)/Release'
    zipAfterPublish: true

- task: PublishBuildArtifacts@1
  displayName: 'Publish Artifact: drop'
  condition: succeeded()
```

This version of *azure-pipelines.yml* looks like the previous version, but it adds two additional tasks.

The first task uses the `DotNetCoreCLI@2` task to *publish*, or package, the app's build results (including its dependencies) into a folder. The `zipAfterPublish` argument specifies to add the built results to a .zip file.

The second task uses the `PublishBuildArtifacts@1` task to publish the .zip file to Azure Pipelines. The `condition`argument specifies to run the task only when the previous task succeeds. `succeeded()` is the default condition, so you don't need to specify it. But we show it here to show its use.

From the integrated terminal, add azure-pipelines.yml to the index, commit the change, and push the change up to GitHub.

```bash
GenaroParedes-MacBook-Pro:mslearn-tailspin-spacegame-web genaroparedes$ git add azure-pipelines.yml
GenaroParedes-MacBook-Pro:mslearn-tailspin-spacegame-web genaroparedes$ git commit -m "Add publish tasks"
[build-pipeline b5b19e3] Add publish tasks
 1 file changed, 13 insertions(+), 4 deletions(-)
GenaroParedes-MacBook-Pro:mslearn-tailspin-spacegame-web genaroparedes$ git push origin build-pipeline
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 516 bytes | 516.00 KiB/s, done.
Total 3 (delta 2), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To https://github.com/ghazaelpo/mslearn-tailspin-spacegame-web.git
   512322e..b5b19e3  build-pipeline -> build-pipeline
```

As you did earlier, from Azure Pipelines, trace the build through each of the steps.

When the pipeline completes, go back to the summary for the build.

Under Related there is 1 published.

![Screen Shot 2021-10-12 at 21.31.32.png](Azure%20Pipelines%20c5a583d4f4cf4ab3b1d0fd426bad78a1/Screen_Shot_2021-10-12_at_21.31.32.png)

Select the artifact, expand the drop folder, you see a *.zip* file that contains your built app and its dependencies:

![Screen Shot 2021-10-12 at 21.32.37.png](Azure%20Pipelines%20c5a583d4f4cf4ab3b1d0fd426bad78a1/Screen_Shot_2021-10-12_at_21.32.37.png)

1. Create Templates.

A template enables you to define common build tasks one time and reuse those tasks multiple times.

I will add this YAML file to create a template:

```bash
parameters:
  buildConfiguration: 'Release'

steps:
- task: DotNetCoreCLI@2
  displayName: 'Build the project - ${{ parameters.buildConfiguration }}'
  inputs:
    command: 'build'
    arguments: '--no-restore --configuration ${{ parameters.buildConfiguration }}'
    projects: '**/*.csproj'

- task: DotNetCoreCLI@2
  displayName: 'Publish the project - ${{ parameters.buildConfiguration }}'
  inputs:
    command: 'publish'
    projects: '**/*.csproj'
    publishWebProjects: false
    arguments: '--no-build --configuration ${{ parameters.buildConfiguration }} --output $(Build.ArtifactStagingDirectory)/${{ parameters.buildConfiguration }}'
    zipAfterPublish: true
```

And then I will call this template from the pipeline adding the below code to azure-pipelines.yml file 

```bash
- template: templates/build.yml
  parameters:
    buildConfiguration: 'Debug'

- template: templates/build.yml
  parameters:
    buildConfiguration: 'Release'
```

When commit the changes the pipeline will run

```bash
git add azure-pipelines.yml templates/build.yml
git commit -m "Support build configurations"
git push origin build-pipeline
```

As the pipeline runs, you see that the process expands the tasks within the template. The tasks that build and publish the project are run two times, once for each build configuration.

![Screen Shot 2021-10-12 at 22.37.29.png](Azure%20Pipelines%20c5a583d4f4cf4ab3b1d0fd426bad78a1/Screen_Shot_2021-10-12_at_22.37.29.png)

When the build completes, go back to the summary page, and select the published artifact as you did before. Expand the drop folder.

You see that the pipeline produces a *.zip* file for both the Debug configuration and the Release configuration.

![Screen Shot 2021-10-12 at 22.38.21.png](Azure%20Pipelines%20c5a583d4f4cf4ab3b1d0fd426bad78a1/Screen_Shot_2021-10-12_at_22.38.21.png)

1. Configure a Schedule release trigger to run each week day (monday to friday) at 3 am just for main branch

![Screen Shot 2021-10-12 at 23.15.29.png](Azure%20Pipelines%20c5a583d4f4cf4ab3b1d0fd426bad78a1/Screen_Shot_2021-10-12_at_23.15.29.png)

![Screen Shot 2021-10-12 at 23.15.55.png](Azure%20Pipelines%20c5a583d4f4cf4ab3b1d0fd426bad78a1/Screen_Shot_2021-10-12_at_23.15.55.png)

[https://dev.azure.com/genaroparedes/Azure Pipelines/_build/results?buildId=5&view=results](https://dev.azure.com/genaroparedes/Azure%20Pipelines/_build/results?buildId=5&view=results)

**Activity 2**

Create a build Classic Pipeline.

## Follow the steps 1 to 5 from the Activity 1 in order to create a Classic Pipeline.

Select GitHub and the Repository that we worked

![Screen Shot 2021-10-12 at 23.01.19.png](Azure%20Pipelines%20c5a583d4f4cf4ab3b1d0fd426bad78a1/Screen_Shot_2021-10-12_at_23.01.19.png)

Create an empty pipeline and add all the required tasks

![Screen Shot 2021-10-13 at 10.03.53.png](Azure%20Pipelines%20c5a583d4f4cf4ab3b1d0fd426bad78a1/Screen_Shot_2021-10-13_at_10.03.53.png)

Finally just run the the Pipeline

![Screen Shot 2021-10-13 at 10.03.40.png](Azure%20Pipelines%20c5a583d4f4cf4ab3b1d0fd426bad78a1/Screen_Shot_2021-10-13_at_10.03.40.png)

File YAML complete 

```bash
# ASP.NET
# Build and test ASP.NET projects.
# Add steps that publish symbols, save build artifacts, deploy, and more:
# https://docs.microsoft.com/azure/devops/pipelines/apps/aspnet/build-aspnet-4

trigger:
- '*'

pool:
  vmImage: 'ubuntu-20.04'
  demands:
  - npm

variables:
  buildConfiguration: 'Release'
  wwwrootDir: 'Tailspin.SpaceGame.Web/wwwroot'
  dotnetSdkVersion: '5.x'

steps:
- task: UseDotNet@2
  displayName: 'Use .NET SDK $(dotnetSdkVersion)'
  inputs:
    version: '$(dotnetSdkVersion)'

- task: Npm@1
  displayName: 'Run npm install'
  inputs:
    verbose: false

- script: './node_modules/.bin/node-sass $(wwwrootDir) --output $(wwwrootDir)'
  displayName: 'Compile Sass assets'

- task: gulp@1
  displayName: 'Run gulp tasks'

- script: 'echo "$(Build.DefinitionName), $(Build.BuildId), $(Build.BuildNumber)" > buildinfo.txt'
  displayName: 'Write build info'
  workingDirectory: $(wwwrootDir)

- task: DotNetCoreCLI@2
  displayName: 'Restore project dependencies'
  inputs:
    command: 'restore'
    projects: '**/*.csproj'

- template: templates/build.yml
  parameters:
    buildConfiguration: 'Debug'

- template: templates/build.yml
  parameters:
    buildConfiguration: 'Release'

- task: PublishBuildArtifacts@1
  displayName: 'Publish Artifact: drop'
  condition: succeeded()
```

## Enable continuous integration for all branches in your repo.

![Screen Shot 2021-10-13 at 9.58.11.png](Azure%20Pipelines%20c5a583d4f4cf4ab3b1d0fd426bad78a1/Screen_Shot_2021-10-13_at_9.58.11.png)

## Configure a Schedule build trigger to run each week day (monday to friday) at 3 am just for main branch.

![Screen Shot 2021-10-13 at 9.57.52.png](Azure%20Pipelines%20c5a583d4f4cf4ab3b1d0fd426bad78a1/Screen_Shot_2021-10-13_at_9.57.52.png)