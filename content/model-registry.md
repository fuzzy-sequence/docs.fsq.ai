---
title: "Model Registry"
linkTitle: "Model Registry"
type: docs
weight: 20
description: >
  Deploying AI capabilities to fleet of devices.
---

Model Registry stores models that can be deployed to edge devices. The models can be pushed from training pipelines or from a marketplace via Model Registry API.

High level integration process:

1. Generate a certificate to sign your models with
2. Upload the certificate using Console or Auth API
3. Start pushing models

It is not required to sing models for development purposes.

## Basic Model Attributes

Every model has a universally unique ID. This UUID is immutable and persistent. UUIDs are used within Fuzzy Sequence to identify models.

Model can also be identified by a pair of name and version. There could be many versions of a model under the same name. The name is mutable and can be changed by the model owner (however it is discouraged). There are no restrictions on the name and version formats.

Each model also has a status defining its lifecycle stage.

## Model Lifecycle in the Registry

After model was added to the registry, the registry will perform model validation and packaging. The latter will create a set of models compatible with supported platforms. After that, the models can be used in the deployment process.