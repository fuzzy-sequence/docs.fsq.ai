---
title: "Model Registry integration with AWS"
linkTitle: "AWS Integration"
weight: 20
---


There are many ways to transfer models from AWS to Fuzzy Sequence.

## AWS Lambda + S3

The simplest way to transfer models from AWS to Fuzzy Sequence is to use
AWS [Lambda](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html) and
[S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html).
The main limitation of this approach is the need to share access to the S3 bucket with Fuzzy Sequence.

To interact with Model Registry API you need to generate API client code. You can use [buf.build](https://buf.build/) or [protoc](https://developers.google.com/protocol-buffers/docs/reference/overview):

{{< tabpane >}}
{{< tab header="python" lang="bash" >}}
python -m grpc_tools.protoc \
  -I path/to/protos \
  --python_out=. --grpc_python_out=. path/to/protos/my.proto
{{< /tab >}}
{{< /tabpane>}}

Here is a sample Lambda function that uploads a model to Fuzzy Sequence:


{{< tabpane >}}
{{< tab header="python"  lang="python" >}}

import grpc
from grpc import ssl_channel_credentials
from my_pb2_grpc import ModelRegistryServiceStub

def upload_mode(event, context):
    # Create SSL credentials using the client certificate, key, and CA certificate (if available)
    ssl_creds = ssl_channel_credentials(
        private_key= open('/path/to/client/key.pem', 'rb').read(),
        certificate_chain= open('/path/to/client/cert.pem', 'rb').read()
    )

    # Create a secure channel using the SSL credentials
    channel = grpc.secure_channel('api.fsq.ai:443', ssl_creds)

    # Use the channel to create a stub for the ModelRegistryService
    stub = ModelRegistryServiceStub(channel)

    # Call a method on the stub to interact with the server
    response = stub.AddModels(request)

def model_upload_handler(event, context):
    return upload_model(event, context)


{{< /tab >}}
{{< tab header="go"  lang="golang" >}}

{{< /tab >}}
{{< /tabpane >}}


## AWS Lambda and Small Models

## Signing a Model 


{{< tabpane >}}
{{< tab header="python"  lang="python" >}}

import boto3
import subprocess
import tempfile

s3 = boto3.client('s3')

def download_file_from_s3(bucket_name, key, local_file_path):
    s3.download_file(bucket_name, key, local_file_path)

def sign_binary(binary_path, cert_file_path, key_file_path, signed_binary_path):
    # Use the openssl command to generate a digital signature of the binary file
    openssl_command = [
        'openssl', 'dgst', '-sha256', '-sign', key_file_path, '-out', signed_binary_path, binary_path
    ]

    # Execute the openssl command and capture the output
    process = subprocess.Popen(openssl_command, stdout=subprocess.PIPE, stderr=subprocess.PIPE)
    stdout, stderr = process.communicate()

    # Check the return code of the openssl command
    if process.returncode != 0:
        # There was an error generating the digital signature
        error_message = f'Error signing binary: {stderr.decode()}'
        raise Exception(error_message)
    else:
        # The digital signature was generated successfully
        success_message = f'Successfully signed binary: {signed_binary_path}'
        print(success_message)

def lambda_handler(event, context):
    # Define the S3 bucket name and key for the binary file
    bucket_name = 'my-bucket'
    key = 'my-binary'

    # Define the path to the certificate file and key file
    cert_file_path = '/path/to/certificate.crt'
    key_file_path = '/path/to/certificate.key'

    # Define the path to the output file for the signed binary
    signed_binary_path = '/path/to/signed/binary'

    # Download the binary file from S3 to a temporary directory
    with tempfile.TemporaryDirectory() as tmpdir:
        local_binary_path = f'{tmpdir}/my-binary'
        download_file_from_s3(bucket_name, key, local_binary_path)

        # Call the sign_binary function to generate the digital signature
        try:
            sign_binary(local_binary_path, cert_file_path, key_file_path, signed_binary_path)
            return {
                'statusCode': 200,
                'body': 'Binary signed successfully'
            }
        except Exception as e:
            return {
                'statusCode': 500,
                'body': str(e)
            }


{{< /tab >}}
{{< /tabpane >}}

