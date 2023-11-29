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
