# Integrating Terraform to CICD tools

1. Create a project in gitlab, then upload an existing terraform repository containing code for Azure or develop from scratch.
    
    [https://gitlab.com/genarop/azure-backend](https://gitlab.com/genarop/azure-backend)
    
    ![Screen Shot 2021-10-15 at 16.04.30.png](Integrating%20Terraform%20to%20CICD%20tools%200a75a8269b98426a9d36235c6856a0e2/Screen_Shot_2021-10-15_at_16.04.30.png)
    

1. Once you previously tested terraform code is in the repository, create a new file named `gitlab-ci.yml`

Click on add button:

![Screen Shot 2021-10-15 at 16.08.56.png](Integrating%20Terraform%20to%20CICD%20tools%200a75a8269b98426a9d36235c6856a0e2/Screen_Shot_2021-10-15_at_16.08.56.png)

- Select the branch
- Select `gitlab-ci.yml`
- Select `template type`
- Look for `terraform` and select

![Screen Shot 2021-10-15 at 16.11.08.png](Integrating%20Terraform%20to%20CICD%20tools%200a75a8269b98426a9d36235c6856a0e2/Screen_Shot_2021-10-15_at_16.11.08.png)

1. Modify the pipeline stages accordingly
    
    ![Screen Shot 2021-10-15 at 16.45.15.png](Integrating%20Terraform%20to%20CICD%20tools%200a75a8269b98426a9d36235c6856a0e2/Screen_Shot_2021-10-15_at_16.45.15.png)
    

1. Setup env variables
    - On the left menu select Settings -> CICD -> Variables
    - Setup the Azure keys
        
        ![Screen Shot 2021-10-15 at 17.04.24.png](Integrating%20Terraform%20to%20CICD%20tools%200a75a8269b98426a9d36235c6856a0e2/Screen_Shot_2021-10-15_at_17.04.24.png)
        
    
2. Make a change to the infrastructure and push the changes to the repository.
    
    ![Screen Shot 2021-10-15 at 18.36.22.png](Integrating%20Terraform%20to%20CICD%20tools%200a75a8269b98426a9d36235c6856a0e2/Screen_Shot_2021-10-15_at_18.36.22.png)
    

![Screen Shot 2021-10-15 at 18.38.11.png](Integrating%20Terraform%20to%20CICD%20tools%200a75a8269b98426a9d36235c6856a0e2/Screen_Shot_2021-10-15_at_18.38.11.png)

![Screen Shot 2021-10-15 at 18.38.22.png](Integrating%20Terraform%20to%20CICD%20tools%200a75a8269b98426a9d36235c6856a0e2/Screen_Shot_2021-10-15_at_18.38.22.png)