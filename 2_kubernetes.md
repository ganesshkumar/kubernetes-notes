# Kubernetes

**Kubernetes(k8s)**, written in Go, evolved from Google's cluster management software, **Borg** and is hosted by **Cloud Native Computing Foundation(CNCF)**.

> Kubernetes is an open-source system for automating deployment, scaling, and management of containerized applications."

## Features

* **Automatic binpacking** - automatically scheduling containers based on resource usage and constraints, with no sacrifice in availability.
* **Self-healing** - automatically replace and reschedules containers from failed nodes, failed heath checks, rules/policy.
* **Horizontal scaling** - automatically scale applications based on resource usage and customer metrics.
* **Service discovery and load balancing** - makes service from set of containers and refers to them via DNS name - automatic discovery of the services and load-balance requests between containers of a given services.
* **Automated rollouts and rollbacks** - roll out and roll back new versions/configurations of an applications without any downtime.
* **Secrets and configuration management** - manage secrets and configuration details for an application without re-building of the entire images.
* **Storage orchestration** - automatically mount local, external and storage solutions to the containers.
* **Batch execution** - supports batch execution.
