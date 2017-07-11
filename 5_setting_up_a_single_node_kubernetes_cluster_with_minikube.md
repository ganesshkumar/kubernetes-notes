# Setting Up a Single-Node Kubernetes Cluster with Minikube

## Requirements for Running Minikube
* Minikube runs as a VM
* To run Minikube on our workstation/laptop, we need
 * kubectl, is a binary to access any Kubernetes cluster
 * On macOS
   * xhyve driver
   * VirtualBox or VMware Fusion hypervisors
 * On Linux
   * VirtualBox or KVM hypervisors
 * On Windows
   * VirtualBox or Hyper-V hypervisors
 * VT-x/AMD-v virtualization must be enabled in BIOS
 * Internet connection on first run.

## Installation  
[VirtualBox](https://www.virtualbox.org/wiki/Downloads),
[xhyve-driver](https://github.com/kubernetes/minikube/blob/master/docs/drivers.md#xhyve-driver),
[kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/),
[minikube](https://github.com/kubernetes/minikube)

```
$ brew cask install virtualbox

$ brew install docker-machine-driver-xhyve

# docker-machine-driver-xhyve need root owner and uid
$ sudo chown root:wheel $(brew --prefix)/opt/docker-machine-driver-xhyve/bin/docker-machine-driver-xhyve
$ sudo chmod u+s $(brew --prefix)/opt/docker-machine-driver-xhyve/bin/docker-machine-driver-xhyve

$ brew install kubectl

$ brew cask install minikube
```

## Running minikube
```
$ minikube start
Starting local Kubernetes v1.6.4 cluster...
Starting VM...
Downloading Minikube ISO
 90.95 MB / 90.95 MB [==============================================] 100.00% 0s
Moving files into cluster...
Setting up certs...
Starting cluster components...
Connecting to cluster...
Setting up kubeconfig...
Kubectl is now configured to use the cluster.

$ minikube status
minikube: Running
localkube: Running
kubectl: Correctly Configured: pointing to minikube-vm at 192.168.99.100

$ minikube stop
```
