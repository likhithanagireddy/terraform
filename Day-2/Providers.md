# Providers
A provider in Terraform is a plugin that enables interaction with an API.
They tell Terraform which services it needs to interact with.

```hcl
provider "aws" {
  region = "us-east-1"
}

Here are some other examples of providers:
- `azurerm` - for Azure
- `google` - for Google Cloud Platform
- `kubernetes` - for Kubernetes
- `openstack` - for OpenStack
- `vsphere` - for VMware vSphere

providers makes Terraform a very versatile tool that can be used to manage a wide variety of infrastructure.

- Different three main ways to configure providers in Terraform:

-- IN the Root module 
The provider configuration block is placed in the root module of the Terraform configuration.
This makes the provider configuration available to all the resources in the configuration.

provider "aws" {
  region = "us-east-1"
}

-- In the child module

You can also configure providers in a child module. This is useful if you want to reuse the same provider configuration in multiple resources.

```hcl
module "aws_vpc" {
  source = "./aws_vpc"
  providers = {
    aws = aws.us-west-2
  }
}

resource "aws_instance" "example" {
  ami = "ami-0123456789abcdef0"
  instance_type = "t2.micro"
  depends_on = [module.aws_vpc]
}
```

-- In the required_providers block

You can also configure providers in the required_providers block. This is useful if you want to make sure that a specific provider version is used.

```hcl
terraform {
  required_providers {
    aws = {
      source = "hashicorp/aws"
      version = "~> 3.79"
    }
  }
}

resource "aws_instance" "example" {
  ami = "ami-0123456789abcdef0"
  instance_type = "t2.micro"
}
```







