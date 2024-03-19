# Deployment presentation

For this activity I will deploy a backend service showing the time and the current pod in use to demonstrate how this service balance the requests.

The first step is start minikube:

![Screen Shot 2021-10-26 at 12.50.19.png](Deployment%20presentation%204e09961d649d4192a1fdf4a625ae463f/Screen_Shot_2021-10-26_at_12.50.19.png)

The source file to achieve this is main.go file, here defines the time and hostname to show:

![Screen Shot 2021-10-26 at 12.16.43.png](Deployment%20presentation%204e09961d649d4192a1fdf4a625ae463f/Screen_Shot_2021-10-26_at_12.16.43.png)

After define the source file we will deploy our Deployment and Service objects using the following file:

![Screen Shot 2021-10-26 at 12.25.28.png](Deployment%20presentation%204e09961d649d4192a1fdf4a625ae463f/Screen_Shot_2021-10-26_at_12.25.28.png)

**Note: It is very important mention that we will take an image already build from Docker Hub.**

The file above is called backend.yml, here we defined two objects, Deployment to build our three pods and Service to access through an IP address.

![Screen Shot 2021-10-26 at 12.30.20.png](Deployment%20presentation%204e09961d649d4192a1fdf4a625ae463f/Screen_Shot_2021-10-26_at_12.30.20.png)

Showing three pods as running, so that means our backend.yml works.

![Screen Shot 2021-10-26 at 12.31.17.png](Deployment%20presentation%204e09961d649d4192a1fdf4a625ae463f/Screen_Shot_2021-10-26_at_12.31.17.png)

Finally we can start our service and see it on Chrome, as you can see, the time is also displayed as well as the pod in use:

![Screen Shot 2021-10-26 at 12.44.13.png](Deployment%20presentation%204e09961d649d4192a1fdf4a625ae463f/Screen_Shot_2021-10-26_at_12.44.13.png)

Even we can compare the pods in use opening two windows at the same time:

![Screen Shot 2021-10-26 at 12.44.30.png](Deployment%20presentation%204e09961d649d4192a1fdf4a625ae463f/Screen_Shot_2021-10-26_at_12.44.30.png)