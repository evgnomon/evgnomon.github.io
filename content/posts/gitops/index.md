---
title: "A Transparent Infrastructure is Functional"
date: 2024-11-02T18:18:28+01:00
categories: ["Teams"]
---
GitOps establishes itself as the core of a functional and declarative infrastructure model, where other tools and platforms become modular, interchangeable components. At its essence, GitOps uses a Git repository as the single source of truth, with infrastructure and application states defined in code. This means any change to the repository triggers automatic updates to deployments, allowing for a streamlined, automated flow without the need for a specific orchestration platform.

By positioning central protocol for GitOps, infrastructure and applications can be managed directly through Git, bypassing intermediaries. Systems with access to Git can quickly pull changes and initiate deployments autonomously after modification. This decentralization makes orchestration platforms optional; instead of dictating workflows, the GitOps protocol enables any compatible tool to plug into the infrastructure, provided it follows the framework.

This structure transforms the ecosystem into a modular environment: GitOps remains the consistent control layer, while orchestration platforms and deployment tools can be swapped or integrated as necessary. In this way, the protocol allows for a truly platform-agnostic model, where Git drives deployments and every other component is flexible, pluggable, and replaceable.

As the deployment protocol is tightly coupled with Git workflow, existing items can get a default semantic making it quick to adopt it for new projects. Forking a new branch, forks the deployment environment which could be used as ephemeral environments for testing or staging. This way, the GitOps protocol can be used to manage the entire lifecycle of an application, from development to production, with a consistent and automated approach out the box.

Using Ansible with GitOps principles over SSH is a straightforward and powerful way to provision and manage virtual machines (VMs) without needing an orchestration platform. Here’s how it works and why it’s effective:

- **Git as Source of Truth**: The infrastructure state (like VM configurations and playbooks) is stored in a Git repository. Any changes, such as updates to VM configurations or environment settings, are committed to this repository, which serves as the single source of truth.

- **SSH as The base Communication Layer**: Ansible connects to VMs over SSH to execute provisioning and configuration tasks directly. When a change is detected in the Git repository, Ansible can be triggered (using a CI/CD pipeline or automation script) to pull the latest configurations and apply them over SSH to the VMs. SSH ensures secure and direct access to each VM without the need for a separate orchestration layer. The control plane is not essential to let the VMs know what to do. This way, the VMs, as the data plane, are entirely independent of the control plane and vice versa.

- **Declarative and Modular Setup**: Each VM’s desired state is defined declaratively in Ansible playbooks and inventory files, making it easy to apply configurations consistently across multiple VMs. Since these configurations are version-controlled in Git, you can track changes and roll back if necessary.

- **Automated and Scalable Provisioning**: With GitOps principles, any update committed to the Git repository can automatically trigger Ansible to reapply configurations across your infrastructure. This allows for scalable, automated provisioning and maintenance without relying on an intermediary platform.

- **Flexibility and Modularity**: Since SSH serves as the main transport layer, any VM or server that supports SSH can be configured, making this approach highly flexible. You can add or remove VMs by updating inventory files in Git, and Ansible will apply changes as needed across your environment.

- **Essential components**: A SQL table implementation and a simple streaming service for messaging layer should be enough to make almost any web application. These components would be selected from stable well known open source projects and the framrwork comes with built-in configuration for them. This way the deployment of a new application would be as simple as adding a new line to the inventory file. This file preferably can be versioned along side the source code of the application.

In summary, using GitOps with Ansible and SSH provides a robust, decentralized infrastructure management approach. Git acts as the source of truth, while Ansible, over SSH, handles provisioning and configuration directly, making it easy to keep VM states consistent and secure. This setup is lightweight, modular, and fully compatible with a wide range of VM environments.

Even without a functional GitOps protocol as a goal, a functional GitOps protocol, as a technique, makes it transparent to manage any other non-functional infrastructure over a set of VMs. So the question always would be why do we need a non-functional infrastructure when stuff which we typically need can be all described using functional protocol and injected as a service.
