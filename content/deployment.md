---
title: "Deployments"
linkTitle: "Deployments"
type: docs
weight: 40
description: >
  Deploying AI capabilities to fleet of devices.
---

To deploy an AI capability onto a device, the latter needs to be connected to the Fuzzy Sequence platform.
See [Fleet Management](/fleet-management) for more information.

Deployment of a capability consists of the following steps:

1. Create a model set for the capability.
2. Identify the device(s) to deploy the capability to. Add these devices to a management group.
3. Create a deployment for the capability and assign it to the management group.

The deployment may span across multiple days or weeks to give enough time for the devices working in the field.


## AI Capability

AI capabilities are components used by the edge device's logic.
These components can be used passively to collect data or actively to inform the device's behavior.
While Fuzzy Sequence provides examples and templates for AI capabilities, it does not provide the logic for the device.
Developers have full control of the logic and their devices' interactions with the platform.

## Model Sets

AI capabilities consist of a set of models and metadata. Model sets are immutable when used in a deployment.
They include specific versions of models to ensure that every devices receives the same exact package.

Metadata adds flexibility to the model set, allowing developers to reference libraries already present on the device.
For example, in the first version of the logic preliminary image processing can be done with OpenCV and
the results passed to more specialized models. The next version of the logic might use specialized model instead of OpenCV.
New model set can use the same firmware to change the AI capability based on metadata.


## Starting a Deployment

