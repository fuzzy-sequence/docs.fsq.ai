---
title: "Getting Started"
linkTitle: "Getting Started"
weight: 10
description: >
  All you need to start using Fuzzy Sequence.
---

Fuzzy Sequence APIs and SDK are in alpha stage. Reach out to us on [fsq.ai](https://fsq.ai) for early access.

As a part of the onboarding process we will provision your mTLS certificate and provide you with the API endpoint and credentials.

Self-signed certificates are supported for development purposes only.



Fuzzy Sequence APIs use gRPC as transport and [buf.build](https://buf.build/fuzzy-sequence/fsq) for code generation and schema versioning.
When access has been provisioned you can use Buf Studio to test the API. Other options:

{{< tabpane >}}
{{< tab header="gRPC Client:" disabled=true />}}
{{< tab header="buf cli"  lang="sh" >}}
buf curl --cert <path your certificate> --key <path to the private key> \
  https://api.fsq.ai/model.v1alpha/ListModels
{{< /tab >}}
{{< tab header="grpc cli" lang="sh" >}}
grpc_cli call --ssl_client_cert <path to certificate> --ssl_client_key <path to private key> \ 
  api.fsq.ai:443 model.v1alpha.ListModels

{{< /tab >}}
{{< tab header="postman"  lang="txt" >}}
Go to "Settings -> Certificates" and add your certificate and private key.
Go to "File -> New -> gRPC Request" and enter the endpoint:
 api.fsq.ai:443
You can choose a method from the drop-down next to the endpoint.
{{< /tab >}}
{{< /tabpane >}}