# Kubernetes Flavors

### Local

This is a way to execute a cluster locally in our system. This way is very helpful to test and learn how cluster works. We can use Minukube to achieve this, this resource will create a cluster of single node.

![Screen Shot 2021-10-26 at 17.29.13.png](Kubernetes%20Flavors%2081fa98f810d54eb1882d157e324621d1/Screen_Shot_2021-10-26_at_17.29.13.png)

### On-prem

Why do organizations choose the path of running Kubernetes in their own data centers, compared to the relative “cake-walk” with public cloud providers? There are typically a few important reasons why an Enterprise may choose to invest in a Kubernetes on-premises strategy:

- Compliance & Data Privacy

It is more secure and some companies can't use public clouds due to data privacy issues.

- Business Policy Reasons

Some enterprises may not be able to utilize public cloud offerings from a specific cloud provider due to their business policies related to competition.

- Cost

This is probably the **most important reason** to run Kubernetes on-premises. Running all of your applications in the public clouds can get pretty expensive at scale.

### Cloud

This is the opposite to On-prem, in this case, we can use a provider cloud if we don't have policies restrictions. This is not recommended to use in big Infrastructures due to the cost.

### Hard-way

Install each of the components separately, without automation or any help, doing everything from scratch, this provide the team more knowledge of what Kubernetes components are working but can take a lot of time.

### Managed

Although Kubernetes is open source, many companies planning to adopt Kubernetes do not have the expertise or resources to set up and maintain the cluster themselves. Managed Kubernetes providers help those looking to use Kubernetes by providing them with the necessary support and maintenance of the Kubernetes clusters. A managed Kubernetes deployment should provide users with a hassle-free control plane, easy deployment options, and ongoing Kubernetes maintenance, enabling users to focus on their business and bringing their apps to market.

What is the reason why we use cloud providers?

Because is an easy way to get an infrastructure for our apps and services. And we can mention a lot of reason such as:

1. Cost Savings
2. Security
3. Flexibility
4. Mobility
5. Insight
6. Increased Collaboration
7. Quality Control
8. Disaster Recovery
9. Loss Prevention
10. Automatic Software Updates
11. Competitive Edge
12. Sustainability

[INGRESS](Kubernetes%20Flavors%2081fa98f810d54eb1882d157e324621d1/INGRESS%200bfb3d9e7ec44fafb2ca5fa20e1de588.md)