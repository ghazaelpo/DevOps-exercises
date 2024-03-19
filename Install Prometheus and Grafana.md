# Install Prometheus and Grafana

### Instructions

- After checking the Installing documentation of Prometheus and the tutorial step by step, you must be able to do your own installation using the provided links as a guide

After the Tools installation such as Grafana and Prometheus we can see that both are working.

I have defined the 9090 Port as per the Tutorial for use and this allow the traffic for Promethus:

![Screen Shot 2021-11-01 at 15.52.07.png](Install%20Prometheus%20and%20Grafana%20fc7db035c3b64f089567c58b5596962d/Screen_Shot_2021-11-01_at_15.52.07.png)

For the Grafana case I have defined the 3000 Port:

![Screen Shot 2021-11-01 at 15.56.38.png](Install%20Prometheus%20and%20Grafana%20fc7db035c3b64f089567c58b5596962d/Screen_Shot_2021-11-01_at_15.56.38.png)

**As you can see both tools are available.**

Even we can make a query to get the metrics from Prometheus:

![Screen Shot 2021-11-01 at 15.59.13.png](Install%20Prometheus%20and%20Grafana%20fc7db035c3b64f089567c58b5596962d/Screen_Shot_2021-11-01_at_15.59.13.png)

 And show a graphic as well:

![Screen Shot 2021-11-01 at 16.00.57.png](Install%20Prometheus%20and%20Grafana%20fc7db035c3b64f089567c58b5596962d/Screen_Shot_2021-11-01_at_16.00.57.png)

In this installation we defined two Targets for both to get metrics from:

![Screen Shot 2021-11-01 at 16.03.39.png](Install%20Prometheus%20and%20Grafana%20fc7db035c3b64f089567c58b5596962d/Screen_Shot_2021-11-01_at_16.03.39.png)

Here is an example of a Dashboard that uses the CPU usage of our node and presents it in Grafana:

![Screen Shot 2021-11-01 at 16.32.56.png](Install%20Prometheus%20and%20Grafana%20fc7db035c3b64f089567c58b5596962d/Screen_Shot_2021-11-01_at_16.32.56.png)

![Screen Shot 2021-11-01 at 16.14.24.png](Install%20Prometheus%20and%20Grafana%20fc7db035c3b64f089567c58b5596962d/Screen_Shot_2021-11-01_at_16.14.24.png)

**In this tutorial, we were able to configure a Prometheus server with two data collectors that are scraped by our Prometheus server which provides the data to build Dashboards with Grafana.**