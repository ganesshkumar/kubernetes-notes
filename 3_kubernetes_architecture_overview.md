# Kubernetes Architecture - Overview

## Main Components
 - Master Nodes (single or multiple)
 - Worker Nodes (single or multiple)
 - Distributed key-value store (like etcd)

[TODO] Diagram

### Master Node
* It is responsible for managing the cluster.
* It is the entry point for all administrative tasks.
* We can communicate with it via CLI, GUI or APIs.

**Multiple Master Nodes** operate in High Availability mode for fault tolerance.
* Only one Master Node will be the leader performing all the operations.
* The rest of the Master Nodes would be followers.

**etcd** is distributed Key-Value store.
* Kubernetes use etcd to manage cluster state. All Master Nodes are connected to etcd.
* etcd can be part of Master Node or configured externally.

A Master Node has the following components:
* **API Server**
 * All administrative tasks are handled by API Server within the Master Node.
 * User sends REST commands to API Server, which is then validated and processed by API Server.
 * The resulting state of the cluster is stored in the key-value store.
* **Scheduler**
 * It schedules work to Worker Nodes taking quality of the service requirements, data locality, affinity, anti-affinity, etc into consideration.
 * It has resource usage information for each Worker Nodes.
 * It knows the constraints that users have set.
 * It schedules the work in terms of Pods and Services.
* **Controller Manager**
 * It manages different non-terminating control loops, which regulates the state of the cluster.
 * Each of these loops knows about the desired state of the objects it manages and watches their current state through API Server.
 * In a control loop, if the current state of objects does not meet the desired state, then the control loop takes steps to make sure that the current state matches the desired state.
* **etcd**
 * It is a distributed key-value store used to store the cluster state.

### Worker Node
* It is the machine(VM, physical server etc.) which runs applications using Pods.
* It has the necessary tools to run Pods and connect them.
* **Pod** is the scheduling unit in Kubernetes and is a collection of one or more containers which are always scheduled together.

[TODO] Diagram

A Worker Node has the following components:
* **Container Runtime**
 * It is needed to run containers.
 * Default container runtime is Docker but can be configured to run rkt.
* **kubelet**
 * It is the agent that runs on Worker Node and communicates with the Master Node.
 * It receives the Pod definition (primarily via API Server) and runs the containers associated with the Pod.
 * It also makes sure that the containers belonging to the Pod are healthy always.
 * The kubelet are currently tightly coupled with Container Runtimes. The WIP Container Runtime Interface(CRI) will make Container Runtimes pluggable in future.
 * [TODO] Diagram
* **kube-proxy**
 * It is the network proxy that runs on each Worker Node and listens to API Server for Service endpoint creation/deletion.
 * For each Service endpoint, kube-proxy sets up the routes so that it can be reached.

 ### State Management with etcd
 * Based of Raft Consensus Algorithm. Raft allows a collection of machines to work as a coherent group that can survive the failures of some of its members. At any given time, one of the nodes in the group will be the Master, and the rest of them will be the Followers. Any node can be treated as a Master.
 * [TODO] Diagram
 * Besides storing cluster state, it can store configuration details such as subnets, ConfigMaps, Secrets etc.

## Network Setup Challenges
* A unique IP is assigned to each Pod.
* Containers in a Pod can communicate to each other.
* The Pod is able to communicate with other Pods in the cluster.
* If configured, the application running in Pod is accessible to external world.
