---
title: "Getting Started"
linkTitle: "Getting Started"
type: docs
weight: 10
description: >
  All you need to start using Fuzzy Sequence.
---

## Get Access

Fuzzy Sequence APIs and SDK are in alpha stage. Reach out to us on [fsq.ai](https://fsq.ai) for early access.
As a part of the onboarding process we will provision your mTLS certificate and provide you with the API endpoint and credentials.

## Generate Certificates

Fuzzy Sequence APIs use mTLS for authentication and encryption. 
For production use cases you will need to provide a valid certificate signed by a CA known to Fuzzy Sequence.

**Self-signed certificates are supported for development purposes only.**

To generate a self-signed certificate use the following command:

```sh
openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 365 -out cert.pem \ 
  -subj "/C=US/ST=State/L=City/O=My Organization/OU=My Unit/CN=mydomain.com"
```

You can use the Console to upload your certificate. Go to "Settings -> Certificates" and click "Upload Certificate".

## API Access

Fuzzy Sequence APIs use gRPC as transport and [buf.build](https://buf.build/fuzzy-sequence/fsq) for code generation and schema versioning.
When access has been provisioned you can use Buf Studio to test the API. Other options:

{{< tabpane >}}
{{< tab header="gRPC Client:" disabled=true />}}
{{< tab header="buf cli"  lang="sh" >}}
buf curl --cert cert.pem --key key.pem https://api.fsq.ai/model.v1alpha/ListModels
{{< /tab >}}
{{< tab header="grpc cli" lang="sh" >}}
grpc_cli call --ssl_client_cert cert.pem --ssl_client_key key.pem \ 
  api.fsq.ai:443 model.v1alpha.ListModels

{{< /tab >}}
{{< tab header="postman"  lang="txt" >}}
Go to "Settings -> Certificates" and add your certificate and private key.
Go to "File -> New -> gRPC Request" and enter the endpoint:
 api.fsq.ai:443
You can choose a method from the drop-down next to the endpoint.
{{< /tab >}}
{{< /tabpane >}}

## Call the API from your Code

After confirming the API can be called from CLI you can start using it from your code.

{{< tabpane >}}
{{< tab header="python" lang="python">}}

import grpc
from grpc import ssl_channel_credentials
from model_pb2_grpc import ModelRegistryServiceStub

ssl_creds = ssl_channel_credentials(
    private_key= open('/path/to/client/key.pem', 'rb').read(),
    certificate_chain= open('/path/to/client/cert.pem', 'rb').read()
)

# Create a secure channel using the SSL credentials
channel = grpc.secure_channel('api.fsq.ai:443', ssl_creds)

# Use the channel to create a stub for the ModelRegistryService
stub = ModelRegistryServiceStub(channel)

# Call a method on the stub to interact with the server
response = stub.ListModels(model_pb2_grpc.ListModelsRequest())
{{< /tab >}}
{{< tab header="c++"  lang="c++" >}}
#include <grpcpp/grpcpp.h>
#include <grpcpp/security/credentials.h>
#include "model_registry_service.grpc.pb.h"

using grpc::Channel;
using grpc::ClientContext;
using grpc::SslCredentialsOptions;
using grpc::SslCredentials;
using grpc::Status;
using fsq::model::v1alpha::ModelRegistryService;
using fsq::model::v1alpha::AddModelsRequest;
using fsq::model::v1alpha::AddModelsResponse;

int main(int argc, char** argv) {
  // Read the private key and certificate chain from files

  std::ifstream key_file("/path/to/client/key.pem", std::ios::binary);
  std::ifstream cert_file("/path/to/client/cert.pem", std::ios::binary);

  std::string key_data((std::istreambuf_iterator<char>(key_file)),
                        std::istreambuf_iterator<char>());

  std::string cert_data((std::istreambuf_iterator<char>(cert_file)),
                        std::istreambuf_iterator<char>());

  // Set up SSL credentials
  SslCredentialsOptions ssl_opts;
  ssl_opts.pem_key_cert_pairs.push_back(
      {key_data, cert_data});
  auto ssl_creds = SslCredentials(ssl_opts);

  // Create a secure channel using the SSL credentials
  auto channel = grpc::CreateChannel("api.fsq.ai:443", ssl_creds);

  // Use the channel to create a stub for the ModelRegistryService
  auto stub = ModelRegistryService::NewStub(channel);

  // Call a method on the stub to interact with the server
  ListModelsRequest request;
  ListModelsResponse response;
  ClientContext context;
  Status status = stub->ListModels(&context, request, &response);
  if (status.ok()) {
    std::cout << "Successfully called ListModels" << std::endl;
  } else {
    std::cerr << "Error calling ListModels: " << status.error_message() << std::endl;
  }

  return 0;
}

{{< /tab >}}
{{< /tabpane >}}


SDK is coming soon!