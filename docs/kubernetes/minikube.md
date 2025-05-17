
## Minikube quick start

After installing minikube ( see [this page](https://minikube.sigs.k8s.io/docs/start) ), you can start a cluster by running:

```sh
minikube start
```

Access the Kubernetes dashboard running within the minikube cluster:

```sh
minikube dashboard
```

Stop your local cluster:

```sh
minikube stop
```



Delete your local cluster:

```sh
minikube delete
```

Delete all local clusters and profiles:

```sh
minikube delete --all
```

## The *pause* containers

The **registry.k8s.io/pause** containers are minimal containers used as "pause" pods in Kubernetes. They serve as the parent process for a pod's network namespace, ensuring that the network stack is consistent and shared by all containers in the pod. 

Specifically, they:

- Set up and hold the network namespace for the pod, allowing the containers within the pod to communicate with each other using localhost.
- Provide a stable network namespace even if the main containers in the pod are restarted.

These containers are lightweight, consuming minimal resources, and their primary function is to act as a placeholder for the pod's lifecycle management. In a Minikube setup, they are automatically created and managed by Kubernetes.


# References

- [Kubectl reference](https://kubernetes.io/docs/reference/kubectl/quick-reference/)
- [Hello Minikube tutorial](https://kubernetes.io/docs/tutorials/hello-minikube/)

