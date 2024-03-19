# Azure Repositories

### Create a new Azure repository.

![Screen Shot 2021-10-12 at 15.02.29.png](Azure%20Repositories%209875e839249942868ac64a4082f723d9/Screen_Shot_2021-10-12_at_15.02.29.png)

![Screen Shot 2021-10-12 at 15.03.03.png](Azure%20Repositories%209875e839249942868ac64a4082f723d9/Screen_Shot_2021-10-12_at_15.03.03.png)

### Upload some code to the repo.

Next to the Repository name click on three dots and then on upload file

![Screen Shot 2021-10-12 at 15.58.38.png](Azure%20Repositories%209875e839249942868ac64a4082f723d9/Screen_Shot_2021-10-12_at_15.58.38.png)

After the previous step just add your file and the comment, then click on Commit button

![Screen Shot 2021-10-12 at 15.59.54.png](Azure%20Repositories%209875e839249942868ac64a4082f723d9/Screen_Shot_2021-10-12_at_15.59.54.png)

The file is already in the Repository

![Screen Shot 2021-10-12 at 16.01.55.png](Azure%20Repositories%209875e839249942868ac64a4082f723d9/Screen_Shot_2021-10-12_at_16.01.55.png)

### Select a branching strategy and execute in azure repos.

I selected Git-Flow strategy to work with my repository. In this case I will clone the Repository to my Local computer to begin with the process.

Git-Flow consist in create a new independent branch and in this branch create another branches called features, so all our changes will on our created branch and not in main.

![Screen Shot 2021-10-12 at 19.09.11.png](Azure%20Repositories%209875e839249942868ac64a4082f723d9/Screen_Shot_2021-10-12_at_19.09.11.png)

First is necessary create the new branch in my case I called Develop

![Screen Shot 2021-10-12 at 18.58.36.png](Azure%20Repositories%209875e839249942868ac64a4082f723d9/Screen_Shot_2021-10-12_at_18.58.36.png)

![Screen Shot 2021-10-12 at 18.59.23.png](Azure%20Repositories%209875e839249942868ac64a4082f723d9/Screen_Shot_2021-10-12_at_18.59.23.png)

For the Git-Flow process is necessary create the new branches based on Develop branch as per the above diagram and then start work there. We could have as many as we want features branches.

![Screen Shot 2021-10-12 at 19.07.14.png](Azure%20Repositories%209875e839249942868ac64a4082f723d9/Screen_Shot_2021-10-12_at_19.07.14.png)

I created two branches, I will perform changes and then create a pull request to main in the next steps but first I will configure Branch policies.

![Screen Shot 2021-10-12 at 19.14.26.png](Azure%20Repositories%209875e839249942868ac64a4082f723d9/Screen_Shot_2021-10-12_at_19.14.26.png)

### Configure Branch policies.

![Screen Shot 2021-10-12 at 19.15.58.png](Azure%20Repositories%209875e839249942868ac64a4082f723d9/Screen_Shot_2021-10-12_at_19.15.58.png)

Locate your branch in the page. You can browse the list or you can search for your branch using the Search all branches box in the upper right

![Screen Shot 2021-10-12 at 19.17.00.png](Azure%20Repositories%209875e839249942868ac64a4082f723d9/Screen_Shot_2021-10-12_at_19.17.00.png)

Select the ... button. Select Branch policies from the context menu

![Screen Shot 2021-10-12 at 19.39.29.png](Azure%20Repositories%209875e839249942868ac64a4082f723d9/Screen_Shot_2021-10-12_at_19.39.29.png)

And finally I will add a require number of reviewers

![Screen Shot 2021-10-12 at 19.38.58.png](Azure%20Repositories%209875e839249942868ac64a4082f723d9/Screen_Shot_2021-10-12_at_19.38.58.png)

### Create a pull request to main branch base on your branch strategy.

**Creating a change in Feature1 Branch**

![Screen Shot 2021-10-12 at 19.25.27.png](Azure%20Repositories%209875e839249942868ac64a4082f723d9/Screen_Shot_2021-10-12_at_19.25.27.png)

**Creating a change in Feature2 Branch**

![Screen Shot 2021-10-12 at 19.26.39.png](Azure%20Repositories%209875e839249942868ac64a4082f723d9/Screen_Shot_2021-10-12_at_19.26.39.png)

Pull Request from Feature1 branch to develop

![Screen Shot 2021-10-12 at 19.30.04.png](Azure%20Repositories%209875e839249942868ac64a4082f723d9/Screen_Shot_2021-10-12_at_19.30.04.png)

Pull Request from Feature2 branch to develop

![Screen Shot 2021-10-12 at 19.33.51.png](Azure%20Repositories%209875e839249942868ac64a4082f723d9/Screen_Shot_2021-10-12_at_19.33.51.png)

Merging previous pull requests in Develop Branch

![Screen Shot 2021-10-12 at 19.43.29.png](Azure%20Repositories%209875e839249942868ac64a4082f723d9/Screen_Shot_2021-10-12_at_19.43.29.png)

And finally merging with main and waiting for reviewer

![Screen Shot 2021-10-12 at 19.44.32.png](Azure%20Repositories%209875e839249942868ac64a4082f723d9/Screen_Shot_2021-10-12_at_19.44.32.png)

![Screen Shot 2021-10-12 at 19.45.10.png](Azure%20Repositories%209875e839249942868ac64a4082f723d9/Screen_Shot_2021-10-12_at_19.45.10.png)

[Azure Pipelines](Azure%20Repositories%209875e839249942868ac64a4082f723d9/Azure%20Pipelines%20c5a583d4f4cf4ab3b1d0fd426bad78a1.md)

[Azure DevOps Introduction](Azure%20Repositories%209875e839249942868ac64a4082f723d9/Azure%20DevOps%20Introduction%20e683d2acccc547dfb9873b3f96d47869.md)