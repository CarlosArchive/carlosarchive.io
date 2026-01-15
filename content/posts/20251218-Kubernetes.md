---
title: "Kubernetes"
summary: 
date: 2025-12-21
series: ["PaperMod"]
weight: 1
aliases: ["/kubernetes-1"]
tags: ["K8s"]
author: ["Carlos A"]
---

Recently, I started an online course in order to understand and reinforce my understanding of the internals of Kubernetes. Needless to say, with work, holidays and changing priorities, I won't be completing this course anytime soon. 

This is intended to be a brief introduction to Kubernetes components, not a manual on how to use it.

## What is Kubernetes?

Kubernetes is a container orchestration system. It extends the benefits of containerisation by allowing users to flexibly deploy and manage containers. Engineers can distribute workloads across their infrastructure through the allocation of resources and separate them using Kubernetes networking features and namespaces.

## Why do we have Kubernetes?

Historically, applications were deployed to physical servers. Having multiple applications deployed to physical servers would create a competition for resources between applications. This was solved by virtualisation, which allowed virtual servers that imitated physical servers to be deployed to a single physical server. This allowed applications to be deployed to their own separate environments, made more easily customisable when managed through virtual servers.

However, virtual servers still imitated bare metal servers. With containers, developers could now create lightweight environments similar to virtual machines but with more relaxed separation of resources. Containers have their own filesystems and are isolated from each other, but share the same host OS kernel. As they are faster to build and deploy compared to VMs, they have become popular in modern software development practices.

## What is Kubernetes made of?

Kubernetes consists of several services that are deployed to your computing resources (physical or virtual). These services combined create a Kubernetes cluster, comprised of a control plane and worker nodes. A control plane consists of the kube-apiserver (which exposes the Kubernetes API), the kube-controller-manager, the etcd key-value store and the kube-scheduler (which is responsible for scheduling Pods onto Nodes). More on the etcd key-value store and the controller-manager later.

## The control plane

The control plane is deployed across the cluster for redundancy. In the past, Kubernetes used to use a master node which contained the control plane, but has since renamed to control plane for architectural accuracy. You might still find a master node when running a smaller local version of Kubernetes using something like minikube.

The kube api-server handles API calls. When you interact with the control plane, you make contact with the kube api-server.

The kube-controller-manager, as it is described, manages controllers. Examples of controllers include the Node controller (a controller which monitors Nodes) and the Job controller (which watches Jobs).

The etcd key-value store stores all cluster data e.g. cluster data, configuration and state information.

The kube-scheduler is responsible for scheduling Pods onto Nodes, using factors such as resource requirements to decide the appropriate destination for each.

## The worker nodes

The worker nodes contain a kubelet, a container runtime and a kube-proxy (optional). The kubelet is an agent that runs on each node in the cluster. It ensures pods are running and communicates back to the control plane. The container runtime is the software responsible for running containers and the kube-proxy contains network rules which enforce things like packet filtering and forwarding.

# References
Official Kubernetes Documentation- kubernetes.io 
