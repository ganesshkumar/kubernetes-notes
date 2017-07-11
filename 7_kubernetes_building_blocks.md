# Kubernetes Building Blocks

Upcoming Terms: Pods, ReplicaSets, Deployments, Namespaces, Labels, Selectors.

## Kubernetes Object Model

These entities describes:
* What containerized applications we are running and on which node
* Application resource consumption
* Different policies attached to applications, like restart/upgrade policies, fault tolerance, etc.

* With each object, we declare our intent or desired state using the `spec` field.
* The Kubernetes system manages the `status` field for objects, in which it records the actual state of the object

* To create an object, we need to provide the spec field to the Kubernetes API Server. The spec field describes the desired state, along with some basic information, like the name.

Sample Deployment Object
```
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.7.9
        ports:
        - containerPort: 80
```

## Pods
* A Pod is the smallest and simplest Kubernetes object.
* It represents single instance of the application.
* A Pod is a logical collection of one or more containers, which
 * Are scheduled together on the same host.
 * Share the same network namespace.
 * Mount the same external storage.

[TODO Diagram]

* Pods can not self-heal, which are handled by controllers(Deployments, ReplicaSets, ReplicationControllers etc.)

## Labels
* Labels are key-value pairs that can be attached to any Kubernetes objects
* Labels are used to organize and select a subset of objects, based on the requirements in place

[TODO Diagram]

## Label Selectors
* **Equality-Based Selectors**
 * =, ==, or != operators
* **Set-Based Selectors**
 * in, notin, and exist operators

## Replication Controllers
* A ReplicationController(rc) is a controller that is part of the Master Node's Controller Manager
* It makes sure the specified number of replicas for a Pod is running at any given point in time.

## ReplicaSets
* A ReplicaSet(rs) is the next-generation ReplicationController.
* ReplicaSets support both equality- and set-based Selectors, whereas ReplicationControllers only support equality-based Selectors.

[TODO Diagram]

* ReplicaSets can be used independently, but they are mostly used by Deployments to orchestrate the Pod creation, deletion, and updates.
* A Deployment automatically creates the ReplicaSets, and we do not have to worry about managing them.

## Deployments
* Deployment objects provide declarative updates to Pods and ReplicaSets.
* The DeploymentController is part of the Master Node's Controller Manager, and it makes sure that the current state always matches the desired state.

[TODO Diagram]
* On top of ReplicaSets, Deployments provide features like Deployment recording, with which, if something goes wrong, we can rollback to a previously known state.

## Namespaces
 * We can partition the Kubernetes cluster into sub-clusters using Namespaces.
 * The names of the resources/objects created inside a Namespace are unique, but not across Namespaces

```
$ kubectl get namespaces
NAME          STATUS    AGE
default       Active    1h
kube-public   Active    1h
kube-system   Active    1h
```

* Generally, Kubernetes creates two default namespaces: kube-system and default.
* The `kube-system` namespace contains the objects created by the Kubernetes system.
* The `default` namespace contains the objects which belong to any other namespace.
* `kube-public` is a special namespace, which is readable by all users and used for special purposes, like bootstrapping a cluster. 
