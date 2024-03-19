# Getting started with Kubernetes

## Core concepts

1. Tell us a brief history (in your own words) about K8S and and why you should learn it

Kubernetes is a open-source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation.

1. What is the reason why we use k8s?

Because is smaller and faster than the old way. The use of images is the best way to deploy an application because you can build service by service to build an entire application using less resources than application on host.

![Screen Shot 2021-10-25 at 17.54.54.png](Getting%20started%20with%20Kubernetes%2092bed57195c242ea848e8ecdbe4a97cc/Screen_Shot_2021-10-25_at_17.54.54.png)

1. What is a pod?

It is the smallest object that you can deploy in Kubernetes

1. What kind of benefits we find with k8s?

Agile application creation and deployment, continuous development, integration, and deployment, environmental consistency across development, testing, and production: Runs the same on a laptop as it does in the cloud, resource utilization: high efficiency and density and environmental consistency across development, testing, and production: Runs the same on a laptop as it does in the cloud.

1. What is the difference between k8s services?

A Kubernetes service is a logical abstraction for a deployed group of pods in a cluster (which all perform the same function). Since pods are ephemeral, a service enables a group of pods, which provide specific functions (web services, image processing, etc.) to be assigned a name and unique IP address (clusterIP).

1. Explain the k8s architecture

The biggest entity of the architecture is the cluster, this include nodes and nodes include services, this last one include pods and as this way the architecture is built.

1. Use an analogy comparing Kubernetes with the real world....like explaining k8s to a kid

Kubernetes is like a car, this car needs different components to work, for example tires, fuel and engine. This way Kubernetes works, you can create a game, the game is the car and all their components will build the game itself. 

1. Explain the Kubernetes flavors, use a table to show advantages & disadvantages

There are two different flavors to setting up a Kubernetes environment: vanilla Kubernetes and managed Kubernetes. With vanilla kubernetes, a software development team has to pull the Kubernetes source code binaries, follow the code path, and build the environment on the machine. On the other hand, managed kubernetes comes pre-compiled and pre-configured with tools that improve features to enhance a certain focus area, such as storage, [security](https://www.containiq.com/post/kubernetes-security-best-practices), deployment, [monitoring](https://www.containiq.com/post/kubernetes-monitoring), etc. Managed Kubernetes versions are also known as Kubernetes distributions.

![Untitled](Getting%20started%20with%20Kubernetes%2092bed57195c242ea848e8ecdbe4a97cc/Untitled.png)

1. Mention some k8s objects/resources (at least 5)

Pods, Namespaces, ReplicationController, ReplicaSet, Deployment, DaemonSet, 

1. Based on your experience....
    1. How would you like to implement the use of k8s in a real-life project? Blog about courses
    2. What kind of resources would you use? Pods, Namespaces, Deployments, ReplicaSet.
    3. Would you make your implementation private or public? Explain why. Public because I would like that everyone have a blog.
    4. What flavor is the best option for this? Managed Kubernetes
    5. What other tools do you need to achieve your implementation?
    
    Docker and Azure.