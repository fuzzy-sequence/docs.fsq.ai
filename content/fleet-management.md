---
title: "Fleet Management"
linkTitle: "Fleet Management"
type: docs
weight: 30
description: >
  Manage your fleet of devices.
---

Fleet Management includes two main components:
1. Edge SDK - A lightweight library that helps to communicate with the Fleet Manager
2. Fleet Manager - A web service that allows you to see the status of your devices and manage them


## Edge SDK

The SDK is used on the device to perform the following interactions:
1. Register the device with the Fleet Manager
2. Report the status of the device
3. Fetch available model set
4. Report the status of the model set deployment

The SDK provides secure and reliable transport for the AI control plane of the device.

## Fleet Manager

The Fleet Manager keeps track of devices interacting with the platform.
It reduces the complexity of managing a fleet of devices by support device groups and automation. 
The fleet can be examined and groups can be created using the Console and the API.
