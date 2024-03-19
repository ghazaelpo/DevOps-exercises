# Build tf+azure image and upload to docker hub

The below is the Built image and pushed to this link:

[https://hub.docker.com/layers/169253526/ghazaelpo/terraform-azure-cli/v1/images/sha256-9ed969118c7967d8b8f0583c730cb892d2e9fbd60a631c79ad13b24cdfa4312e?context=repo&tab=layers](https://hub.docker.com/layers/169253526/ghazaelpo/terraform-azure-cli/v1/images/sha256-9ed969118c7967d8b8f0583c730cb892d2e9fbd60a631c79ad13b24cdfa4312e?context=repo&tab=layers)

```bash
#Install Ubuntu
FROM ubuntu:20.10

COPY . .

#From Ubuntu inside use apt-get to install the required packages
RUN apt-get update -y && apt-get install -y sudo && apt-get install -y curl && apt-get install -y unzip

RUN apt-get install -y gnupg2

#Install Azure cli

RUN curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash

#Install Terraform

RUN curl https://releases.hashicorp.com/terraform/0.12.24/terraform_0.12.24_linux_amd64.zip | unzip

RUN mkdir terraform 
RUN mv terraform ~/bin
```