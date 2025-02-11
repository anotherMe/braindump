
# Kubernetes

## Minikube basic controls

NOTE: After a (rather superficial) research on pros and cons of different Kubernetes development environments [Minikube vs. k3d vs. kind vs. Getdeck](https://www.blueshoe.io/blog/minikube-vs-k3d-vs-kind-vs-getdeck-beiboot/), we opted for **Minikube**.

Start a cluster by running:

minikube start
Access the Kubernetes dashboard running within the minikube cluster:

minikube dashboard

Stop your local cluster:

minikube stop
Delete your local cluster:

minikube delete
Delete all local clusters and profiles

minikube delete --all


## The *pause* containers

The **registry.k8s.io/pause** containers are minimal containers used as "pause" pods in Kubernetes. They serve as the parent process for a pod's network namespace, ensuring that the network stack is consistent and shared by all containers in the pod. 

Specifically, they:

- Set up and hold the network namespace for the pod, allowing the containers within the pod to communicate with each other using localhost.
- Provide a stable network namespace even if the main containers in the pod are restarted.

These containers are lightweight, consuming minimal resources, and their primary function is to act as a placeholder for the pod's lifecycle management. In a Minikube setup, they are automatically created and managed by Kubernetes.