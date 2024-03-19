# Azure Monitoring

### Activity 1

Answer the following questions regarding Azure Monitoring with your own words:

- ¿Why is it helpful to use Azure Monitor in our projects?

Because we can measure all the data from our applications. This information help us to understand how the applications are working and identify issues using this data.

Azure Monitor is very helpful for analyze all the data from your resources in the platform, such as Virtual Machines, Virtual Networks, Network Interface Cards, etc.

One of the most important things regarding this tool is that you can offer Support operations using alerts and automated actions.

- ¿What data does Azure Monitor collects?

Azure monitor collects data from applications, operating systems, Azure Resources, Azure Subscriptions, Azure Tenant and Custom Sources.

- ¿What is Log Analytics in Azure?

It is a tool to interact with data collected from Azure monitor, you can edit and run log queries to analyze all the information.

- ¿Why is it helpful to create a Log Analytics Workspace for the alerts?

Because you can handle all your information and work with that, even you can show the information using charts. The information from Log Analytics is very helpful, even you can set rules.

### Activity 2

Configure alert rules with Azure Monitor.

**For this exercise I will use a Virtual Machine I already created from previous exercise**

![Screen Shot 2021-10-06 at 9.18.44.png](Azure%20Monitoring%208b5d3650775f4d69924c13ee57b6263c/Screen_Shot_2021-10-06_at_9.18.44.png)

**Go to Azure Monitor and create three different alert rules**

To set an alert is necessary follow the below steps:

1. From home page go to Monitor
    
    ![Screen Shot 2021-10-06 at 9.49.47.png](Azure%20Monitoring%208b5d3650775f4d69924c13ee57b6263c/Screen_Shot_2021-10-06_at_9.49.47.png)
    

1. In monitor overview select Alerts section
    
    ![Screen Shot 2021-10-06 at 9.52.14.png](Azure%20Monitoring%208b5d3650775f4d69924c13ee57b6263c/Screen_Shot_2021-10-06_at_9.52.14.png)
    

1. Once Clicked alerts section just go to Create a new alert rule
    
    ![Screen Shot 2021-10-06 at 10.05.11.png](Azure%20Monitoring%208b5d3650775f4d69924c13ee57b6263c/Screen_Shot_2021-10-06_at_10.05.11.png)
    
2. First we have to select the resources that we want to apply an alert to monitoring, in this case I have chosen a Virtual Machine called "Activity3-vm-1"
    
    ![Screen Shot 2021-10-06 at 10.08.14.png](Azure%20Monitoring%208b5d3650775f4d69924c13ee57b6263c/Screen_Shot_2021-10-06_at_10.08.14.png)
    
3. The next section is add any condition that you want, in this case I have set up an alert to activate when the VM has restarted
    
    ![Screen Shot 2021-10-06 at 10.13.43.png](Azure%20Monitoring%208b5d3650775f4d69924c13ee57b6263c/Screen_Shot_2021-10-06_at_10.13.43.png)
    
4. After that we need create an action group, just click in create action group
    
    ![Screen Shot 2021-10-06 at 10.20.26.png](Azure%20Monitoring%208b5d3650775f4d69924c13ee57b6263c/Screen_Shot_2021-10-06_at_10.20.26.png)
    

1. Then just we have to set up the alert as per below, select the Notification type, name and configure our mail to receive the alert
    
    ![Screen Shot 2021-10-06 at 10.24.41.png](Azure%20Monitoring%208b5d3650775f4d69924c13ee57b6263c/Screen_Shot_2021-10-06_at_10.24.41.png)
    
2. If you have complete the set up for your alert just trigger it by your configure action. I restarted the Virtual Machine and received the email that I have set up.
    
    ![Screen Shot 2021-10-06 at 10.40.51.png](Azure%20Monitoring%208b5d3650775f4d69924c13ee57b6263c/Screen_Shot_2021-10-06_at_10.40.51.png)
    

1. I configured two more alerts, Start VM and Run Command on VM

![Screen Shot 2021-10-06 at 10.45.30.png](Azure%20Monitoring%208b5d3650775f4d69924c13ee57b6263c/Screen_Shot_2021-10-06_at_10.45.30.png)

![Screen Shot 2021-10-06 at 10.46.14.png](Azure%20Monitoring%208b5d3650775f4d69924c13ee57b6263c/Screen_Shot_2021-10-06_at_10.46.14.png)