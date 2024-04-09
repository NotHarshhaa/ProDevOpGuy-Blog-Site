---
author: "H A R S H H A A"
title: ☸️ Usefull Kubernetes tricks for DevOps Engineer 🎩🪄
description: "💫 Most usefull Kubernetes tricks that are helpful! for any DevOps Engineer 💫"
date: "2024-04-09"
template: "post"
draft: false
slug: "Usefull-Kubernetes-Tricks"
series:
  - "DevOps"
tags:
  - "DevOps"
  - "Kubernetes"
  - "Tips&Tricks"
hidemeta: false
comments: false
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
cover:
    image: "images/kubernetes-tricks.png" # image path/url
    relative: true # when using page bundles set this to true
    hidden: false # only hide on current single page
---

## 💫 Most usefull Kubernetes tricks that are helpful! for any DevOps Engineer 💫

### ➡️𝗚𝗲𝘁𝘁𝗶𝗻𝗴 𝗦𝘁𝗮𝗿𝘁𝗲𝗱

---

#### 1. Graceful Pod Shutdown with PreStop Hooks

**PreStop** hooks allow for the execution of specific commands or scripts inside a pod just before it gets terminated. This capability is crucial for ensuring that applications shut down gracefully, saving state where necessary, or performing clean-up tasks to avoid data corruption and ensure a smooth restart.

---

#### 2. Automated Secret Rotation with Kubelet

**Kubernetes** supports the automatic rotation of secrets without restarting the pods consuming these secrets. This feature is particularly useful for maintaining security standards by regularly changing sensitive information without impacting the application’s availability.

---

#### 3. Debugging Pods with Ephemeral Containers

**Ephemeral containers** provide a way to temporarily attach a debug container to a running pod without changing its original specification. This is immensely helpful for debugging live issues in a production environment where you cannot afford to disrupt service.

---

#### 4. Node Affinity for Workload-Specific Scheduling

**Node affinity** allows you to specify rules that limit which nodes your pod can be scheduled on, based on labels on nodes. This is useful for directing workloads to nodes with specific hardware (like GPUs), ensuring data locality, or adhering to compliance and data sovereignty requirements.

---

#### 5. Pod Priority and Preemption for Critical Workloads

**Kubernetes** allows you to assign priorities to pods, and higher priority pods can preempt (evict) lower priority pods if necessary. This ensures that critical workloads have the resources they need, even in a highly congested cluster.

---

#### 6. Efficient Resource Management with Requests and Limits

**Kubernetes** allows you to specify CPU and memory (RAM) requests and limits for each container in a pod. Requests guarantee that a container gets the specified amount of resources, while limits ensure a container never uses more than the allotted amount. This helps in managing resource allocation efficiently and preventing any single application from monopolizing cluster resources.

---

#### 7. Custom Resource Definitions (CRDs) for Extending Kubernetes

**CRDs** allow you to extend Kubernetes with your own API objects, enabling the creation of custom resources that operate like native Kubernetes objects. This is powerful for adding domain-specific functionality to your clusters, facilitating custom operations, and integrating with external systems.

---

## Support 🫶

- Help spread the word about **ProDevOpsGuy** by sharing it on social media and recommending it to your friends. 🗣️
- You can also sponsor 🏅 on [Github Sponsors](https://github.com/sponsors/NotHarshhaa)
