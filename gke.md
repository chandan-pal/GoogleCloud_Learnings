
# Google Kubernetes Engine
## Hypervisor
The software layer that breaks the dependencies of an operating system on the underlying hardware and allows several virtual machines to share that hardware is called a a hypervisor.

Kernel-based Virtual Machine, or KVM, is one well-known hypervisor.

## Container
Containers are isolated user spaces for running application code. The user space is all the code that resides above the kernel, and it includes applications and their dependencies.

Containers are lightweight because they don’t carry a full operating system.
They can be scheduled or integrated tightly with the underlying system.

The application code is packaged with all the dependencies it needs, and the engine that executes the container is responsible for making them available at runtime.

## Container images
An application and its dependencies are called an image, and a container is simply a running instance of an image.

By building software into container images, developers can package and ship an application without worrying about the system it will run on.

Docker is one way to build containers.
But Docker does not offer way to orchestrate those applications at scale like kubernetes does.

- Linux Process : Each linux process has its own virtual memory address space. Linux process can be rapidly created and destroyed.
- Linux Namespace : Containers use Linux namespace to control what an application can see, such as process ID numbers, directory trees, IP addresses etc.
- Linux cgroups : control what an application can use, such as maximum consumption of CPU time, memory, I/O bandwidth etc.

Container use union file systems to bundle everything needed into a neat package.

A container image is structured in layers, and the tool used to build the image reads instructions from a file called container manifest.
For Docker container image that is Dockerfile.

When launching a new container from an image, the container runtime adds a new writable layer on top of the underlying layers. All changes made to the running container, such as writing new files, modifying existing files, and deleting files, are written to this thin writable container layer. This layer is ephemeral, which means that when the container is deleted, the contents of this writable layer are lost.

Google maintains Artifact Registry at **pkg.dev** which contains public open source images.
It also provides place to store private images which are integrated with IAM.

## Kubernetes
open source platform for managing containerized workloads and services. It makes it easy to orchestrate many containers on many hosts, scale them as microservices, and easily deploy rollouts and roollbacks.

At the highest level, Kubernetes is a set of APIs that you can use to deploy containers on a set of nodes called a cluster.

The Kubernetes system is divided into a set of primary components
1. one that run as the control plane
2. other set of nodes that run containers

A node represents a computing instance, like a machine.

Kubernetes supports declarative configurations.

## Google Kubernetes Engine
GKE is managed kubernetes service hosted on Google's infrastructure. It's designed to help deploy, manage and scale Kuberbernetes services hosted on google's infrastructure.

Google Kubernetes Engine offers a mode of operation called GKE Autopilot, which is designed to manage your cluster configuration, like nodes, scaling, security, and other preconfigured settings.

The GKE auto-upgrade feature ensures that clusters are always upgraded with the latest stable version of Kubernetes.

The virtual machines that host containers in a GKE cluster are called nodes.

GKE has a node auto-repair feature that was designed to repair unhealthy nodes.

It performs periodic health checks on each node of the cluster and nodes determined to be unhealthy are drained and recreated.

Just like Kubernetes supports scaling workloads, GKE supports scaling the cluster itself.

GKE is integrated with several services: Cloud Build uses private container images securely stored in Artifact Registry to automate the deployment.

GKE is integrated with several services: 
- Cloud Build uses private container images securely stored in Artifact Registry to automate the deployment.
- IAM helps control access by using accounts and role permissions.
- Cloud Monitoring provides an understanding into how an application is performing.
- Virtual Private Clouds, which provide a network infrastructure including load balancers and ingress access for your cluster.
- Google Cloud console provides insights into GKE clusters and their resources, and a way to view, inspect, and delete resources in those clusters.

### Kubernetes components
Kubernetes cluster needs two types of virtual machines.
1. Control Panel
   - fleet of cooperating processes that make a kubernetes cluster work.
   - They coordinate the entire cluster

	- Kube-APIServer
	  - accept commands that view or change the state of the cluster.
	  - also authenticates incoming requests, determines whether they are authorized and valid, and manages admission control.
	 - kubectl
		  - The job of the kubectl command is to connect to the kube-APIserver and communicate with it using the Kubernetes API.
	  - etcd
		  - Its job is to reliably store the state of the cluster.
		  - This includes all the cluster configuration data,along with more dynamic information such as what nodes are part of the cluster, what Pods should be running, and where they should be running.
	- kube-scheduler
	  -  responsible for scheduling Pods onto the nodes.
	  -  It evaluates the requirements of each individual Pod and selects which node is most suitable. However, it doesn’t do the work of actually launching Pods on nodes
     - Kube-controller-manager
		- it continuously monitors the state of a cluster through the kube-APIserver.
		- Whenever the current state of the cluster doesn’t match the desired state, kube-controller-manager will attempt to make changes to achieve the desired state.
	- Node Controller
		- job is to monitor and respond when a node is offline.



2. Nodes
   - The node’s job is to run Pods.
   - Each node runs a small family of control-plane components called a kubelet.
   - Kubelet
   	- kubelet is like Kubernetes’s agent on each node.
   	- When the kube-APIserver wants to start a Pod on a node, it connects to that node’s kubelet.
   	- Kubelet uses the container runtime to start the Pod and monitors its lifecycle, including readiness and liveness probes, and reports back to the kube-APIserver.
- kube-proxy
	- maintains network connectivity among the Pods in a cluster

### Kubernetes Object Management
All kubernetes objects are identified by a unique name and a unique identifier.
The objects which are needed in kubernetes can be declared and maintained with manifest files. These manifest can be written in YAML or JSON.

Essentially these manifest file defines a desired state for a Pod (its name and a specific container image for it to run)
required fieds - 
- apiVersion : states the kubernetes API version.
- kind : states the object e.g. Pod
- metadata : defines the object name

All objects are identified by a name. Name must consist of unique string under 253 characters. Every object created throughout the life of a cluster has a unique identifier, or UID, generated by Kubernetes.

Labels are key-value pairs to tag objects during or after their creation. Labels help identify and organize objects.

## GKE Autopilot
- Optimizes the management of kubernetes with a hands-off experience.
- Less management overhead
- Only pay for what you use
- With Autopilot, Google is fully responsible for optimizing resource consumption.
- less configuration options
- Autopilot clusters also have restrictions on access to node objects.
- Features like SSH and privilege escalation were removed and there are limitations on node affinity and host access.

## GKE Standard
- The standard mode allows the kubernetes management infrastucture to be configured in many different ways.
- With GKE standard, you pay for all of the provisioned infrastructure, regardless of how much gets used.


## Kube-ctl
command line utility used by administrators to control Kubernetes clusters. It is used to communicate with the kube API server on the control plane.
It transform the command line entries into API calls and send them to the kube API server.

kube-ctl needs cluster credentials to connect to a cluster. The GKE cluster credentials can be fetched by gcloud command "get-credentials".

Kube-ctl is a tool for administering the internal state of an existing cluster, it can’t create new clusters or change the shape of existing clusters.

Kubectl command syntax is composed of four parts
1. the command - like get, describe, logs or exec.
2. the type - kubernetes object type like Pods, deployments, nodes etc.
3. the name - the name of the object
4. optional flags - 

e.g.
**get pod** : get list of Pods in a cluster.



