# Service Registry

### What is Consul

Consul is a solution that allow handle networking and security challenges of operating microservices and cloud infrastructure. It is very useful to manage all your microservices on a single platform and also offers additional benefits such as failure handling, retries, and network observability. 

### Consul Architecture

Consul is a distributed system designed to run on a cluster of nodes. A node can be a physical server, cloud instance, virtual machine, or container. Connected together, the set of nodes Consul runs on is called a datacenter. Within the datacenter, Consul can run in two modes server or client. Server agents maintain the consistent state for Consul. Clients are a light-weight process that run on every node where services are running. A datacenter will have between 3 - 5 servers and many clients.

The Consul architecture is a system designed to run on a cluster of nodes. A node can be a physical server, cloud instance, virtual machine, or container.

### Installing Consul

### Service registration and discovery