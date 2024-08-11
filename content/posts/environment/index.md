---
title: "Environment and Lightweight Branches"
date: 2024-08-11T17:36:28+01:00
categories: ["Technique"]
---
![Environment](environment.png)

As everything is code, borrowing cloud resources are also code. Like VMs or Database servers, storage accounts etc.
These resources sometime requires manual intervention if that is not automated yet.
An environment owns all resources. This is to make sure production resources can be fully isolated from the rest of resources for governance purpose.

As the environment owns resources, which means it triggers lifecycle events including accusation and return events. We can not have branches doing the same thing unless each branches maps to a single environment which is not optimal. As there could be always expensive resources like computing and network resources associated with the environment and that is not needed to be replicated upon adding a new branch. So branching should be always light as a rule of thumb.

So a code repository has a few isolated environments and each environment gets a range of branches deployed at the same time. So the application code should always consider that resources are created with proper configs to eliminate collisions. For example network ports could be mapped to the same machine in different branches so it should be considered that the port should be different per branch.

Branches are light weight environments which are mapped to the same environment with different settings. Each branch can optionally come with a shadow environment to test deployment scripts. The prod environment could have a staging as the shadow. There could be ephemeral environments which optionally can have a shadow.
