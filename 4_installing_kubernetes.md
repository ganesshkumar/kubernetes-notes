# Installing Kubernetes

## Kubernetes Configuration
* All-in-One Single-Node Installation
  - for learning, development and testing.
* Single-Node etcd, Single-Master and Multi-Worker Installation
* Single-Node etcd, Multi-Master and Multi-Worker Installation
* Multi-Node etcd, Multi-Master and Multi-Worker Installation
  - advanced and recommended production setup.

## Infrastructure for Kubernetes Installation
* Bare-metal, public cloud or private cloud?
* RHEL, CoreOS, CentOS or something else?
* Which networking solution should we use?
* etc.

## Localhost Installation
There are a few localhost installation options available to deploy single- or multi-node Kubernetes clusters:
* Minikube
* Ubuntu on LXD

## On-Premise Installation
* **On-Premise VMs**
 * Kubernetes can be installed on VMs created via Vagrant, VMware vSphere, KVM, etc.
 * There are different tools available to automate the installation, like Ansible or kubeadm.
* **On-Premise Bare Metal**
 * Kubernetes can be installed on on-premise Bare Metal, on top of different Operating Systems, like RHEL, CoreOS, CentOS, Fedora, Ubuntu, etc.
 * Most of the tools used to install VMs can be used with Bare Metal as well.

## Cloud Installation

* **Hosted Solutions** - any given software is completely managed by the provider.
 * Google Container Engine (GKE)
 * Azure Container Service
 * OpenShift Dedicated
 * Platform9
 * IBM Bluemix Container Service
* **Turnkey Cloud Solutions** - we can deploy a solution or software with just a few commands.
 * Google Compute Engine
 * Amazon AWS
 * Microsoft Azure
 * Tectonic by CoreOS
* **Bare Metal**
Kubernetes can be installed on Bare Metal provided by different cloud providers.

## Kubernetes Installation Tools/Resources
* **kubeadm**
 * It is a secure and recommended way to bootstrap the Kubernetes cluster.
 * It has a set of building blocks to setup the cluster, but it is easily extendable to add more functionality
* **kubespray**
  * Helps to install Highly Available Kubernetes clusters on AWS, GCE, Azure, OpenStack, or Bare Metal.
  * It is based on Ansible, and is available on most Linux distributions
* **kops**
 * Helps to create, destroy, upgrade, and maintain production-grade, highly-available Kubernetes clusters from the command line.
 * It can provision the machines as well(early stage)
