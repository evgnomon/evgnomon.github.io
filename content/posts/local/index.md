---
title: "Local"
date: 2024-02-05T13:00:28+01:00
categories: ["Technique"]
---
![Local](local.webp)

We haven't yet printed anything in space, so we cannot use it to verify independence from the factory. Independence needs to be verified without relying on the printed space and without the need to be in the factory. This is where localization comes into play. We should be able to check the correctness of a change locally before submitting it. That way, we can continue making changes even when we are restricted within the factory.

We don't need a production-ready local environment, or a complete local setup. We don't even need an entirely printable local environment! What we need is for the next change to be verifiable locally. So, we are not halted locally when the time comes that we are terminated in the factory. As soon as we get the next printable product, we start using that product instead. But we don't have to wait for that to build up an entirely printable world.

This way, the factory would still need to receive changes from us, since we are the ones who choose which factory we want to submit changes to. We maintain the independence to produce the next correct change.

Verifying locally does not mean emulation or simulation, as the verification must be sound and complete to ensure the next change is valid. The submitted change does not have to undergo further checks to ensure it can integrate. Thus, the local environment uses components from a production system but is not deployed and accessible to any user except a single developer, using a single machine in the while verifying the change. It can be distroyed afterward.

The challenge lies in parts that are not accessible locally. In such cases, another component, which is available locally, should be used as a replacement. If no local component is available to provide the same API, that component should not be exposed in the code. This is because we cannot verify the code locally in that situation. However, that component could still be used, but it should be disabled while the application delivers the rest of its functionalities. Such a component should be integrated as a plugin.
