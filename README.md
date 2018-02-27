# AWS API Gateway - Nodes JS - Lambda - Custom Authorizer for IP Ranges

## Description

This is a lambda function that will return an `Unauthorized` response unless the sourceIp is in the supplied IP ranges


## Lambda Install and Configuration

### Prerequisites
You will need:
 - Node v6 and later and NPM installed (an appropriately recent version will do)

### Install
1. `git clone` the latest version of the source code
1. run `npm install` to download the dependancies
1. Create a zip file of the directory (ensure index.js is in the root directory of the zip file (not in a subdirectory))
1. Create an AWS Lambda function with a very basic execute role (the function does not require any additional access beyond any logging you may want to configure), the function does not require a VPC to run
1. Load the zip file into the AWS Lambda function's code

### Configuration
You must set an environment variable `AUTHORIZED_IP_RANGE` to be the comma separated list of CIDR IP ranges that are authorized to execute the function. Example:
`192.168.1.0/24,111.112.113.114/32`
> Ranges MUST be in CIDR range format - use /32 for single IPs


## API Gateway Configuration

Configure a custom lamba Authorizer, Lambda Event Payload of Request

Disable Authorization Caching (or ensure the Caching is based on the Source IP address)

Set the `authorization` on the `settings` page under `method request` for the resource you want to protect
