# Lab 1, lets install K8s, Helm and my very first chart

### Instructions

- By any means of infrastructure (VMs, AWS, GCP, DigitalOcean), you will create a kubernetes clusters, then, using helm, you will deploy an nginx controller, as an extra task, you will deploy cert-manager.

**I will use Azure Cloud to this activity, as first step is necessary create a Cluster**

1. But first I will create a resource group to handle this activity
    
    ![Screen Shot 2021-10-27 at 16.51.17.png](Lab%201,%20lets%20install%20K8s,%20Helm%20and%20my%20very%20first%20ch%2039340398eed643aabda087a12c7180bf/Screen_Shot_2021-10-27_at_16.51.17.png)
    

1. In this resource group I will create a cluster
    
    ![Screen Shot 2021-10-27 at 16.53.39.png](Lab%201,%20lets%20install%20K8s,%20Helm%20and%20my%20very%20first%20ch%2039340398eed643aabda087a12c7180bf/Screen_Shot_2021-10-27_at_16.53.39.png)
    
    ![Screen Shot 2021-10-27 at 16.58.40.png](Lab%201,%20lets%20install%20K8s,%20Helm%20and%20my%20very%20first%20ch%2039340398eed643aabda087a12c7180bf/Screen_Shot_2021-10-27_at_16.58.40.png)
    
2. Once we have created the cluster is necessary connect to it using Azure CLI
    
    ![Screen Shot 2021-10-27 at 17.00.59.png](Lab%201,%20lets%20install%20K8s,%20Helm%20and%20my%20very%20first%20ch%2039340398eed643aabda087a12c7180bf/Screen_Shot_2021-10-27_at_17.00.59.png)
    
    ![Screen Shot 2021-10-27 at 17.10.50.png](Lab%201,%20lets%20install%20K8s,%20Helm%20and%20my%20very%20first%20ch%2039340398eed643aabda087a12c7180bf/Screen_Shot_2021-10-27_at_17.10.50.png)
    

**Adding the Helm Repository**

After the previous cluster configuration I will add the Helm repository

![Screen Shot 2021-10-27 at 17.15.02.png](Lab%201,%20lets%20install%20K8s,%20Helm%20and%20my%20very%20first%20ch%2039340398eed643aabda087a12c7180bf/Screen_Shot_2021-10-27_at_17.15.02.png)

**Installing the Chart**

To create a simple NGINX ingress controller without customizing the defaults, I will use helm.

![Screen Shot 2021-10-28 at 11.17.31.png](Lab%201,%20lets%20install%20K8s,%20Helm%20and%20my%20very%20first%20ch%2039340398eed643aabda087a12c7180bf/Screen_Shot_2021-10-28_at_11.17.31.png)

After the installation we can consult the if the load balancer was generated.

![Screen Shot 2021-10-28 at 11.25.47.png](Lab%201,%20lets%20install%20K8s,%20Helm%20and%20my%20very%20first%20ch%2039340398eed643aabda087a12c7180bf/Screen_Shot_2021-10-28_at_11.25.47.png)

So no we are ready to proceed with a Demo.

### **Run demo applications**

To see the ingress controller in action, I will run two demo applications in our AKS cluster. In this example, I will use `kubectl apply` to deploy two instances of a simple *Hello world* application.

I'm going to create two files with different names:

![Screen Shot 2021-10-28 at 11.33.29.png](Lab%201,%20lets%20install%20K8s,%20Helm%20and%20my%20very%20first%20ch%2039340398eed643aabda087a12c7180bf/Screen_Shot_2021-10-28_at_11.33.29.png)

![Screen Shot 2021-10-28 at 11.33.47.png](Lab%201,%20lets%20install%20K8s,%20Helm%20and%20my%20very%20first%20ch%2039340398eed643aabda087a12c7180bf/Screen_Shot_2021-10-28_at_11.33.47.png)

![Screen Shot 2021-10-28 at 11.34.07.png](Lab%201,%20lets%20install%20K8s,%20Helm%20and%20my%20very%20first%20ch%2039340398eed643aabda087a12c7180bf/Screen_Shot_2021-10-28_at_11.34.07.png)

We run the two demo applications using `kubectl apply`:

![Screen Shot 2021-10-28 at 11.37.49.png](Lab%201,%20lets%20install%20K8s,%20Helm%20and%20my%20very%20first%20ch%2039340398eed643aabda087a12c7180bf/Screen_Shot_2021-10-28_at_11.37.49.png)

### **Create an ingress route**

Both applications are now running on our Kubernetes cluster. To route traffic to each application, we will create a Kubernetes ingress resource. The ingress resource configures the rules that route traffic to one of the two applications.

We define our ingress using the below *hello-world-ingress.yaml* file:

![Screen Shot 2021-10-28 at 11.43.02.png](Lab%201,%20lets%20install%20K8s,%20Helm%20and%20my%20very%20first%20ch%2039340398eed643aabda087a12c7180bf/Screen_Shot_2021-10-28_at_11.43.02.png)

Create the ingress resource using the `kubectl apply -f hello-world-ingress.yaml` command.

![Screen Shot 2021-10-28 at 11.46.16.png](Lab%201,%20lets%20install%20K8s,%20Helm%20and%20my%20very%20first%20ch%2039340398eed643aabda087a12c7180bf/Screen_Shot_2021-10-28_at_11.46.16.png)

### **Testing the ingress controller**

To get your external IP you can go directly to the Azure Portal and search your cluster and then go to Services and ingresses to finally copy your LoadBalancer Address:

![Screen Shot 2021-10-28 at 11.51.33.png](Lab%201,%20lets%20install%20K8s,%20Helm%20and%20my%20very%20first%20ch%2039340398eed643aabda087a12c7180bf/Screen_Shot_2021-10-28_at_11.51.33.png)

Or you can get using the terminal:

![Screen Shot 2021-10-28 at 11.53.07.png](Lab%201,%20lets%20install%20K8s,%20Helm%20and%20my%20very%20first%20ch%2039340398eed643aabda087a12c7180bf/Screen_Shot_2021-10-28_at_11.53.07.png)

Once you have your External IP you can go to the web browser and test it:

![Screen Shot 2021-10-28 at 11.56.57.png](Lab%201,%20lets%20install%20K8s,%20Helm%20and%20my%20very%20first%20ch%2039340398eed643aabda087a12c7180bf/Screen_Shot_2021-10-28_at_11.56.57.png)

![Screen Shot 2021-10-28 at 11.57.18.png](Lab%201,%20lets%20install%20K8s,%20Helm%20and%20my%20very%20first%20ch%2039340398eed643aabda087a12c7180bf/Screen_Shot_2021-10-28_at_11.57.18.png)

[Screen Recording 2021-10-28 at 12.01.04.mov](Lab%201,%20lets%20install%20K8s,%20Helm%20and%20my%20very%20first%20ch%2039340398eed643aabda087a12c7180bf/Screen_Recording_2021-10-28_at_12.01.04.mov)