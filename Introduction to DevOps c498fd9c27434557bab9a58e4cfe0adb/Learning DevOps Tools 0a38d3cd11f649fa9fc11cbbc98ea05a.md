# Learning DevOps Tools

# 02 - Learning DevOps Functions and Tools

## By Mario Robles, Akira Lopez, Carlos Catalán, Genaro Paredes, Alberto Valle & Octavio Palacios.

**Make a team of 2 people and for each of the following DevOps functions**

- **Collaboration**
    
    **Communication** **and collaboration** are some of the key cultural aspects of DevOps. Using DevOps tools and automating the software delivery process establishes collaboration by physically linking development and operations workflows and responsibilities.
    
    **Tools for DevOps collaboration:**
    
    - **Slack:** Slack is a team communication tool co-founded by Stewart Butterfield Eric Costello Cal Henderson and Serguei Mourachov. Slack began as an internal tool used by their company Tiny Speck in the development of Glitch a now-defunct online game. Slack was launched in August 2013 and signed up 8000 customers within 24 hours of launch.
    - **Microsoft Teams:** Microsoft Teams is a unified communication and collaboration platform that combines persistent workplace chat video meetings file storage (including collaboration on files) and application integration.
    - **Stack Overflow:** Stack Overflow for Teams is a better way to collaborate and share knowledge across your organization.
    - **Atlassian Confluence:** Confluence is content and team collaboration software that changes how modern teams work.
    - **Mattermost:** *Open Source.* ****Mattermost is an open-source self-hosted Slack alternative. Mattermost is: Slack-compatible not Slack-limited \'96 Mattermost features rival Slack features and supports a superset of Slack\'92s incoming and outgoing webhook integrations including compatibility with existing Slack integrations.
    
- **Continuous Integration**
    
    ***Continuos Integration*** is a DevOps practice that allows multiple developers to contribute and collaborate on a shared code base at a fast pace. Without this integration, collaboration between developers becomes a manual and tedious process of coordinating mergers and code updates. Also it could bring a lot of issues.
    
    **Tools for DevOps Integration:**
    
    - **Jenkins:** *Open Source.* Jenkins It’s an excellent choice if your organization needs local support to handle sensitive customer data, such as HIPAA compliance data. Also it allows automating builds and tests quickly.
    - **TeamCity: Y**ou can run parallel builds at the same time, mark your builds and identify the hung ones. TeamCity is easy to install and its interface is really user-friendly. ****
    - **Bamboo: I**s a server-based CI and deployment tool from AtlassianBamboo allows building new branches automatically and merging them after the testing. With this tool, continuous deployment and delivery are easy to reach.
    - **GitLab CI:** *Open Source.* This highly scalable tool is easy to install and set up for projects hosted on GitLab thanks to GitLab API. Apart from testing projects and building them, GitLab CI can deploy builds. This tool points out the areas that need improvement in the development process.
    - **Buddy: I**s a DevOps automation platform that allows continuous integration, continuous deployment and feedback. This tool was made for working with projects that use code from the Bitbucket and GitHub repositories. Buddy is a commercial tool with a straightforward, user-friendly interface and minimalistic material design.
    
- **Configuration**
    
    **Configuration** **management** software enables the use of tested and proven software development practices for managing and provisioning data centers in real-time through plaintext definition files. 
    
    **Tools for DevOps Integration:**
    
    - **Ansible**: is a radically simple IT automation platform that makes your applications and systems easier to deploy. Avoid writing scripts or custom code to deploy and update your applications—automate in a language that approaches plain English, using SSH, with no agents to install on remote systems.
    - **CFEngine**: Its primary function is to provide automated configuration and maintenance of large-scale computer systems.
    - **Puppet:** an automated administrative engine for Linux, Unix, and Windows systems, performs administrative tasks such as adding users, installing packages, and updating server configurations based on a centralized specification.
    - **Chef**: It manages servers in the cloud, on-premises, or in a hybrid environment. Being cloud-agnostic lets you manage both the data center and cloud environments at once, even as you change your cloud providers.
    - **Salt Stack:** salt is a scalable configuration management and orchestration tool. DevOps teams use salt to manage IT environments, such as data centers, through event-driven orchestration and remote execution of configurations.
    
- **Containers**
    
    Containers are a form of virtualization of the operating system. Only one of these can be used to run from a microservice to complex software processes. The main functions of containers are: isolating and preserving applications, services, processes, executables, libraries, codes, and necessary configuration files.
    
    Unlike traditional VMs and servers, containers do not have the image of the operating system, this makes them much lighter and, therefore, a much lower resource overload.
    
    Let's check a couple of tools we can use to work with Containers:
    
    - **Dockers**
        
        It is an **open-source project** that automates the deployment of applications inside software containers by providing an additional layer of abstraction and automation of operating-system-level virtualization on Linux. Docker uses resource isolation features of the Linux kernel such as cgroups and kernel namespaces to allow independent "containers" to run within a single Linux instance avoiding the overhead of starting and maintaining virtual machines.
        
    
    - **Kubernets**
        
        It is an **open-source system** for managing containerized applications across multiple hosts providing basic mechanisms for deployment maintenance and scaling of applications.
        
    - **RED HAT OPENSHIFT**
        
        OpenShift is a platform as a service product from Red Hat. It is also an Infrastructure as a Service (IaaS) comparable to Google Storage and Amazon S3 online storage services.
        
    
    - **AMAZON ECS**
        
        Amazon Elastic Container Service (Amazon ECS) is a highly scalable **high-performance container orchestration service** that supports Docker containers and allows you to easily run and scale containerized applications on AWS. Amazon ECS eliminates the need for you to install and operate your own container orchestration software manage and scale a cluster of virtual machines or schedule containers on those virtual machines.
        
    
    - **AZURE AKS**
        
        Azure Kubernetes Service (AKS) makes it simple to deploy a managed Kubernetes cluster in Azure. AKS reduces the complexity and operational overhead of managing Kubernetes by offloading much of that responsibility to Azure. As a hosted Kubernetes service Azure handles critical tasks like health monitoring and maintenance for you.
        
- **Orchestration**
    
    ***Orchestration*** is the automation of numerous tasks that run at the same time in a way that minimizes production issues and time to market. This process is based on container concept and share each other a close relation. It is very useful because allow save resources and manage in a same place. **We can find the same tools for both containers and orchestration.** 
    
    - **Docker swarm** (not open source) also offers a set of utilities for launching, organizing, and managing a container cluster. A Docker Swarm is a group of either physical or virtual machines that are running the Docker application and that have been configured to join together in a cluster.
        
        ![image.png](Learning%20DevOps%20Tools%200a38d3cd11f649fa9fc11cbbc98ea05a/image.png)
        
    - **Kubernetes** is an open source container management system designed and published by Google. It is used to create a distributed cluster of hosted containers. Kubernetes provides robust container clustering tools that include health monitoring, deployment, failover, and autoscaling.
        
        ![Img1DocAndKub.png](Learning%20DevOps%20Tools%200a38d3cd11f649fa9fc11cbbc98ea05a/Img1DocAndKub.png)
        
    
    - **Amazon Elastic Container Service** (not open source) is an Amazon cloud-based service that makes it easy to manage Docker containers in a cluster. ECS has a powerful API and is tightly integrated with the rest of Amazon's cloud suite, enabling powerful DevOps workflows.
        
        ![ecs.png](Learning%20DevOps%20Tools%200a38d3cd11f649fa9fc11cbbc98ea05a/ecs.png)
        
    
    - **Apache Mesos** is a cluster management tool developed by Apache that can efficiently perform container orchestration. The Mesos framework is open-source, and can easily provide resource sharing and allocation across distributed frameworks.
    - **Azure Service Fabric** is a Platform-as-a-Service solution that lets developers focus on business logic and application development by making container deployments, packaging and management a lot easier. Service Fabric lets companies deploy and manage microservices across distributed machines, allowing the management of both stateful and stateless services. It also integrates seamlessly with CI/CD tools to help manage application life cycles while letting you create and manage clusters across different environments, including Linux, Windows Server, Azure on-premises and other public cloud offerings.

---

- **Monitoring**
    
    It's very important to monitor the architectures, applications and all the outputs that our project can generate, this to create metrics that help us compare performance, alerts in case of an emergency and anticipate any problem that may arise in the future.
    
    - **Grafana and Prometheus:**
        
        When it comes to monitoring **infrastructure** the most popular options are **Grafana** and **Prometheus**.
        
        Both are Open Source and are usually used together connecting them to have a better visualization of the data.
        
        **Prometheus** specializes more in the monitoring of events while **Grafana** complements it in the visualization of data, alerts, etc.
        
        ![grafana.png](Learning%20DevOps%20Tools%200a38d3cd11f649fa9fc11cbbc98ea05a/grafana.png)
        
    - **Jaeger and New Relic:**
        
        **Jaeger** and **New Relic** are **Application Performance Management (APM)** that help us detect latencies and problems in our distributed system. It is useful when our system is installed in different data centers.
        
        Both are Open Source 
        
        ![jaeger.png](Learning%20DevOps%20Tools%200a38d3cd11f649fa9fc11cbbc98ea05a/jaeger.png)
        
    - **Logstash (Logs Management):**
        
        **Logstash** is part of Elastic Stack (Also it can be used independently) and is an Open Source tool that allows us to centralize information such as **Logs**, normalize and redistribute it.
        
        ![lohstash.jpeg](Learning%20DevOps%20Tools%200a38d3cd11f649fa9fc11cbbc98ea05a/lohstash.jpeg)
        

---

- **Security**
    
    ***DevOps security*** is a practice of safeguarding the entire DevOps environment, also should enable a productive DevOps ecosystem, while helping to identify and remediate code vulnerabilities and operational weaknesses long before they become an issue.
    
    **Tools for DevOps security:**
    
    - **OWASP ZAP:**
        
        It can help you automatically find security vulnerabilities in your web applications while you are developing and testing your applications. It's also a great tool for experienced pentesters to use for manual security testing.
        
    - **SonarQube:** *Open Source.* SonarQube is an automatic code review tool to detect bugs, vulnerabilities and code smells in your code. It integrates with development teams’ native workflows to provide them with continuous code inspection across all of their project branches and pull requests.
    - **HASHICORP VAULT:** HashiCorp's Vault secures stores and controls access to tokens passwords certificates API keys and other sensitive resources in modern datacenters. For each resource Vault handles leasing revocation rolling and auditing.
    - **DIGITAL.AI APP PROTECTION:** When addressed properly with application protection security solutions – including JavaScript protection, threat detection and limiting API connections to known good sites, along with defensive measures that can shut down application functionality in the event of an attack –effective application security enables customers to detect and protect against active threats, shielding businesses and consumers from data breaches and financial losses.
    - **Aqua Security:** Aqua security helps save the day, providing container security throughout the DevSecOps pipeline. Aqua’s cloud-native security platform provides users with full control over containerized environments, with tight runtime security controls and intrusion prevention capabilities, at scale.