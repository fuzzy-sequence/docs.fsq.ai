---
title: "Overview"
linkTitle: "Overview"
weight: 5
description: >
  General  information about Fuzzy Sequence and its use cases. Start here to learn where Fuzzy Sequence fits in your workflow.
resources:
- src: "**data-sci*.png"
- src: "**uav*.png"
- src: "**drone*.png"
---

Artificial Intelligence (AI) is an essential component for businesses 
seeking to remain competitive in today's market.
The majority of AI products are designed with a cloud-centric approach.
However, these products may not be readily accessible to certain critical industries.
There are several use cases where the cloud is not a good fit for cloud-based AI:

- unstable internet connection (e.g. remote areas)
- costs of data transfer (e.g. video streaming to the cloud)
- privacy concerns and regulations (e.g. GDPR)
- latency (e.g. real-time applications)

These use cases require running compute on the edge devices, such as cameras, sensors, robots, drones, etc.
To make AI accessible to these use cases, we need to build AI apps that run on the edge devices.

## Why Fuzzy Sequence?

Fuzzy Sequence offers a platform for deploying and managing AI capabilities that run on the edge devices.
The goal of this platform is to help the business to build and run AI-powered devices at scale.
The platform is designed to be used by data scientists, hardware manufacturers, integrators and solution providers.

1. The platform detaches the control plane from the data plane.
   It only helps to manage AI Capabilities leaving developers in **full control of the data** and their devices' behavior.
2. The platform minimizes the need to **change the firmware** of the devices.
   This decreases the risks of bricking the device while providing up-to-date AI capabilities.
3. The platform is designed for uses cases with **unstable connectivity and field conditions**.
   The deployments are expected to run for many days and weeks.
4. Security and privacy are at the core of the platform.
   The platform support **model signing and traffic encryption**.

## For Data Scientists

Fuzzy Sequence helps the data scientists and researchers
to monetize and expand the reach of their AI models
by deploying them to fleets of edge devices. Learn more about [Model Registry](/docs/model-registry/).

{{< imgproc data-sci Resize "500X280" />}}


For data scientist interested in specific applications
Fuzzy Sequence allows to incorporating Edge AI devices into the MLOps processes.
The Edge fleet becomes a part of their IaaS solution.
Learn more about integrations with public cloud providers: [AWS](/docs/tutorials/aws/), [Azure](/docs/tutorials/azure/), [GCP](/docs/tutorials/gcp/).


## For Hardware Manufacturers

Fuzzy Sequence simplifies the process of building AI-powered devices. 

This helps businesses to improve performance of their existing products through deployment of ready-to use edge-optimized AI models.

{{< imgproc uav Resize "500X185" />}}

In addition to this Fuzzy Sequence enables businesses to build new specialized products minimizing installation and operation costs.

{{< imgproc drone Resize "500X185" />}}

## For Integrators and Solution Providers

Connection [Model Registry](/docs/model-registry/),
[Fleet Management Agent](/docs/device-fleet-management/) and [Console](/docs/console) allows to radically simplify deployment and management
of AI-powered capabilities at scale.
It fills in the gap between RnD and production, driving implementation costs down.

