# INGRESS

### **Set up Ingress on Minikube with the NGINX Ingress Controller**

In this case I will use Katakoda terminal as you can see below, this allow us create a  cluster:

![Screen Shot 2021-10-27 at 11.32.25.png](INGRESS%200bfb3d9e7ec44fafb2ca5fa20e1de588/Screen_Shot_2021-10-27_at_11.32.25.png)

To enable the NGINX Ingress controller, run the following command:

![Screen Shot 2021-10-27 at 11.40.51.png](INGRESS%200bfb3d9e7ec44fafb2ca5fa20e1de588/Screen_Shot_2021-10-27_at_11.40.51.png)

Verify that the NGINX Ingress controller is running:

![Screen Shot 2021-10-27 at 11.42.06.png](INGRESS%200bfb3d9e7ec44fafb2ca5fa20e1de588/Screen_Shot_2021-10-27_at_11.42.06.png)

### **Deploy a hello, world app**

Create a Deployment using the following command:

![Screen Shot 2021-10-27 at 11.44.04.png](INGRESS%200bfb3d9e7ec44fafb2ca5fa20e1de588/Screen_Shot_2021-10-27_at_11.44.04.png)

Expose the Deployment:

![Screen Shot 2021-10-27 at 11.44.46.png](INGRESS%200bfb3d9e7ec44fafb2ca5fa20e1de588/Screen_Shot_2021-10-27_at_11.44.46.png)

Verify the Service is created and is available on a node port:

![Screen Shot 2021-10-27 at 11.45.29.png](INGRESS%200bfb3d9e7ec44fafb2ca5fa20e1de588/Screen_Shot_2021-10-27_at_11.45.29.png)

Visit the Service via NodePort:

![Screen Shot 2021-10-27 at 11.51.34.png](INGRESS%200bfb3d9e7ec44fafb2ca5fa20e1de588/Screen_Shot_2021-10-27_at_11.51.34.png)

After get our service web go to the following section:

![Screen Shot 2021-10-27 at 11.53.32.png](INGRESS%200bfb3d9e7ec44fafb2ca5fa20e1de588/Screen_Shot_2021-10-27_at_11.53.32.png)

Use the port get from:

```bash
minikube service web --url
```

![Screen Shot 2021-10-27 at 12.13.39.png](INGRESS%200bfb3d9e7ec44fafb2ca5fa20e1de588/Screen_Shot_2021-10-27_at_12.13.39.png)

And show the test

![Screen Shot 2021-10-27 at 12.14.01.png](INGRESS%200bfb3d9e7ec44fafb2ca5fa20e1de588/Screen_Shot_2021-10-27_at_12.14.01.png)

### Create an Ingress

The following manifest defines an Ingress that sends traffic to your Service via hello-world.info.

Create `example-ingress.yaml` from the following file:

```bash
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: example-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /$1
spec:
  rules:
    - host: hello-world.info
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: web
                port:
                  number: 8080
```

![Screen Shot 2021-10-27 at 12.00.30.png](INGRESS%200bfb3d9e7ec44fafb2ca5fa20e1de588/Screen_Shot_2021-10-27_at_12.00.30.png)

Create the Ingress object by running the following command:

![Screen Shot 2021-10-27 at 12.01.06.png](INGRESS%200bfb3d9e7ec44fafb2ca5fa20e1de588/Screen_Shot_2021-10-27_at_12.01.06.png)

Verify the IP address is set:

![Screen Shot 2021-10-27 at 12.03.12.png](INGRESS%200bfb3d9e7ec44fafb2ca5fa20e1de588/Screen_Shot_2021-10-27_at_12.03.12.png)

Add the following line to the bottom of the `/etc/hosts` file on your computer (you will need administrator access):

![Screen Shot 2021-10-27 at 12.05.46.png](INGRESS%200bfb3d9e7ec44fafb2ca5fa20e1de588/Screen_Shot_2021-10-27_at_12.05.46.png)

Verify that the Ingress controller is directing traffic:

![Screen Shot 2021-10-27 at 12.06.18.png](INGRESS%200bfb3d9e7ec44fafb2ca5fa20e1de588/Screen_Shot_2021-10-27_at_12.06.18.png)

### **Create a second Deployment**

Create another Deployment using the following command:

![Screen Shot 2021-10-27 at 12.07.04.png](INGRESS%200bfb3d9e7ec44fafb2ca5fa20e1de588/Screen_Shot_2021-10-27_at_12.07.04.png)

Expose the second Deployment:

![Screen Shot 2021-10-27 at 12.07.55.png](INGRESS%200bfb3d9e7ec44fafb2ca5fa20e1de588/Screen_Shot_2021-10-27_at_12.07.55.png)

### **Edit the existing Ingress**

Edit the existing `example-ingress.yaml` manifest, and add the following lines at the end:

```bash
- path: /v2
        pathType: Prefix
        backend:
          service:
            name: web2
            port:
              number: 8080
```

Apply the changes:

![Screen Shot 2021-10-27 at 12.09.33.png](INGRESS%200bfb3d9e7ec44fafb2ca5fa20e1de588/Screen_Shot_2021-10-27_at_12.09.33.png)

### **Test your Ingress**

![Screen Shot 2021-10-27 at 12.10.13.png](INGRESS%200bfb3d9e7ec44fafb2ca5fa20e1de588/Screen_Shot_2021-10-27_at_12.10.13.png)