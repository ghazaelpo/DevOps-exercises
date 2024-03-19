# Build tf+aws image and upload to docker hub

The below is the Built image and pushed to this link:

[https://hub.docker.com/layers/169229022/ghazaelpo/aws_cli_terraform/v1/images/sha256-efcc66bbe50f5e1597bdf651cbb7c11e064c05fcd027e267fccd4244accdd86c?context=repo](https://hub.docker.com/layers/169229022/ghazaelpo/aws_cli_terraform/v1/images/sha256-efcc66bbe50f5e1597bdf651cbb7c11e064c05fcd027e267fccd4244accdd86c?context=repo)

```bash
#Install Ubuntu
FROM ubuntu:20.10

COPY . .

#From Ubuntu inside use apt-get to install the required packages
RUN apt-get update -y && apt-get install -y sudo && apt-get install -y curl && apt-get install -y unzip

RUN apt-get install -y gnupg2

#Install aws cli
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"

RUN unzip awscliv2.zip && ./aws/install -i /usr/local/aws-cli -b /usr/local/bin

#Install Terraform

RUN curl https://releases.hashicorp.com/terraform/0.12.24/terraform_0.12.24_linux_amd64.zip | unzip

RUN mkdir terraform 
RUN mv terraform ~/bin
```