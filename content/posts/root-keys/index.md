---
title: "The Root Key"
date: 2024-04-26T08:24:28+02:00
categories: ["Security"]
---
![Secrets](root-key.webp)

Information is typically public unless it is designated as controlled. A secret is information with restricted access. This access can be revoked through access control mechanisms. Secrets are maintained by rotation; when a secret is rotated, its access is simultaneously revoked. Therefore, a secret can be defined as a piece of information that is subject to rotation and is essential for accessing other resources. Each secret is assigned a unique identifier, allowing us to distinguish it from other information. The identifier serves purely as a label, encoded in a finite number of bits.

There exists a root entity whose secret is readable but not rotated by any other entity. Contrarily, if a secret is readable by an entity, then another entity capable of rotating it must exist, unless it pertains to the root entity. To rotate a secret, a parent entity utilizes a secondary secret, named differently from the child's secret. Without a parent secret, the child’s secret cannot be rotated, ensuring that there is always a parent with its own secret.

This mechanism can be described as a lookup algorithm. Each identified entity is either new or previously known. If the algorithm reaches a point where no new entity can be identified, it implies that all entities have been accounted for. The algorithm cannot conclude without identifying a root entity, suggesting that while the number of entities is finite, the number of secrets is potentially infinite. Therefore, there is always an additional secret required for rotation, and we never possess enough bits to access it, ensuring that there is always one more secret that remains unreadable to maintain the rotation of existing secrets. A contradiction, as secrets are in rotation by definition.

If the algorithm continually identifies new entities, this suggests an unending presence of secrets beyond the reach of all identified entities. This reinforces the necessity for an additional secret for each rotation, beyond our capacity to access, ensuring the continuity of secret rotations. A contradiction, as secrets are in rotation by definition.

The lookup algorithm concludes by identifying all entities as either root entities or entities rotated by a root entity.

However, the existence of multiple root entities raises a question. If a secret is rotated but not yet accessed by a child entity, it disrupts the sequence. Thus, a child entity must decide whether to become a root entity or agree to the terms under which the secret continues to rotate. Since a child can change its parent, it can also modify the terms of rotations.

This raises a further question: Assuming that changing parents is possible, what determines the direction in which children switch parents? Control seems to lie in rotation, and the direction would logically be opposite to that of gaining control through rotation. Thus, theultimate root entity always retains control over all other rotations, meaning control and rotation are inherently linked in the root entity not the other way around.

Inspired by this, create a root secret that is inaccessible to others, also store a soft version protected by a password in commodity storage as a backup plan. The hardware version, secured with a PIN and a backup key for self-healing, serves as a security token. Hence, authorization of three public keys is necessary wherever access to the root entity is required. This ensures protection of the key, allowing for the PIN to be rotated along with all related secrets to recover from a breach. Automate this recovery plan. So neither loosing the hardware key, the pin or the soft key will result in a loss of the root key. And no one would have access to the soft version of the private key unless for recovery. And loss of hardware doesn't trigger recovery as there is a backup hard key already. Losing one key doesn't put us in a state without having a backup as there is always one more key for back up beside one operational.

An interesting observation is the increased frequency of rotations, indicating that secrets are rotating more swiftly than any selected frequency, depending on the scale. And anytime reading the secret might give a different result as the key might have rotated just before.
