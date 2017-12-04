# Services
[Lot of images for this section]
Service is a logical grouping of Pods and an associated policy to access them

## Connecting Users to Pods
* Pods are ephemeral in nature, resources like IP addresses allocated are not static(mostly due to a pod dies and recreated)
* So we can not rely on pod's IP address to connect to it, so we use service
* selectors are used to group the pods into a service

Service object example
```
kind: Service
apiVersion: v1
metadata:
  name: frontend-svc
spec:
  selector:
    app: frontend
  ports:
    - protocol: TCP
      port: 80
      targetPort: 5000
```
Service is listening on port 80 while pods are listening on port 5000

* The IP address of the service is routable only within the cluster
* Service also load balances the requests while selecting the pod for it

## kube-proxy
* kube-proxy is a daemon what watches the API server for addition and removal of Services and endopoints
* For a new Service, kube-proxy configures the IPtables rules to capture the trafic for its ClusterIP(Service IP) and forward it to one of the endpoints
* When a Service is removed, the kube-proxy removes the entries from the IPtables

## Service Discovery
Kubernetes supports two ways of discovering Services at their runtime

### Environment Variables
* As soon as a Pod starts, the kubelet daemon witll set a environmental variables in the Pod for all active Services
* The problem with this approach is that the Pods will not have environmental variables for Services that are created after the Pod

### DNS
* Kubernetes has an add-on for DNS, which creates a DNS record for each Service
 * its format is like my-svc.my-namespace.svc.cluster.local
* Servies in the same namespace can reach each other with their name
* Pods in other namespaces have to use namespace:service to access a Service in another namespace

## Service Type
* Which creating a Service, we can choose an access scope for it
 * is only accessible within the cluster
 * is accessible from within the cluster and external world
 * maps to an external entity which resides outside the cluster
* Access scope is decided by ServiceType

### ClusterIP
* It is the default option
* A Service gets its Virtial IP using the ClusterIP
* This IP address is accessible only within the cluster

### NodePort
* In addition to ClusterIP, a port from the range 30000-32767 is mapped to the respective service
* It is useful when we want our Service to be accessible to the external world

### LoadBalancer
* NodePort and ClusterIP Services are automatically created, and the external load balancer will route to them
* The Services are exposed at a static port on each Worker Node
* The Service is exposed externally using the underlying Cloud provider's load balancer feature (It will work only if the Cloud provider supports load balancer)

### ExternalIP
* A Service can be mapped to an ExternalIP address if it can route to one or more of the Worker Nodes. Traffic that is ingressed into the cluster with the ExternalIP (as destination IP) on the Service port, gets routed to one of the the Service endpoints.
* ExternalIPs are not managed by Kubernetes. The cluster administrators has configured the routing to map the ExternalIP address to one of the nodes

### ExternalName
* It has no Selectors or endpoints
* When accessed within the cluster, it returns a CNAME record of an externally configured service.
* Used to make externally configured services like my-database.example.com available inside the cluster
