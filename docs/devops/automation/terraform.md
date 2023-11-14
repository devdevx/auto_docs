# Terraform

## Links

[Tutorial AWS Provider](https://hector-reyesaleman.medium.com/terraform-aws-provider-everything-you-need-to-know-about-multi-account-authentication-and-f2343a4afd4b)
[Course](https://courses.devopsdirective.com/terraform-beginner-to-pro/lessons/03-basic-terraform-usage/03-terraform-plan-apply-destroy)

## Install

### Ubuntu

```bash
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
sudo apt-get update && sudo apt-get install terraform
terraform -help
```

## Commands

```bash
terraform init
terraform apply -auto-approve
terraform destroy -auto-approve
terraform plan
```

Format

```bash
terraform fmt -diff
```

## Files

### `*.tfvars` files

Used to define values for variables.

Terraform will automatically load the variable values from the variable definition file if it is named `terraform.tfvars` or ends in `.auto.tvfars` and placed in the same directory as the other configuration files. Other can be load using the flag `-var-file=<FILE>` .

Example:

`test-env.tfvars`

```
project        = "generated-area-284017"
region         = "europe-west1-b"
cluster_name   = "test-cluster"
node_pool_name = "test-node-pool"
num_nodes      = 0
```

### `variables.tf`

Used to define variables and default values.

````
variable "project" {
  type        = string
  description = "Google project id"
}

variable "region" {
  type        = string
  description = "Google location"
}

variable "cluster_name" {
  type        = string
  description = "Cluester name"
}

variable "node_pool_name" {
  type        = string
  description = "Node pool name"
}

variable "num_nodes" {
  type        = number
  description = "Node pool name"
}
````

### `versions.tf`

Defines the version

```
terraform {
  required_version = ">= 0.12.26"
}
```

### `*.tf` files

Contains code to execute

## File layout example

```
stage
  + vpc
  + services
      + frontend-app
      + backend-app
  + data-storage
      + mysql
      + redis
prod
  + vpc
  + services
      + frontend-app
      + backend-app
  + data-storage
      + mysql
      + redis
mgmt
  + vpc
  + services
      + bastion-host
      + jenkins
global
  + iam
  + s3
```

## Reusable definitions

`modules/services/webserver-cluster/main.tf`

```
resource "aws_security_group" "elb" {
  name = "${var.cluster_name}-elb"
  ingress {
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}
```

`modules/services/webserver-cluster/variables.tf`

```
variable "cluster_name" {
  description = "The name to use for all the cluster resources"
  type        = string
}
```

`modules/services/webserver-cluster/outputs.tf`

```
output "asg_name" {
  value       = aws_autoscaling_group.example.name
  description = "The name of the Auto Scaling Group"
}
```

 `prod/services/webserver-cluster/main.tf`

```
provider "aws" {
  region = "us-east-2"
}
module "webserver_cluster" {
  source = "../../../modules/services/webserver-cluster"
  
  cluster_name = "webservers-prod"
}

resource "aws_autoscaling_schedule" "scale_out_business_hours" {
  autoscaling_group_name = module.webserver_cluster.asg_name
}
```

## Version control

Is recomended to have 2 repositories, one with the live configuration and other with the reusable modules

```
module "webserver_cluster" {
  source = "github.com/foo/modules/services/webserver-cluster?ref=v0.0.1"
  cluster_name  = "webservers-stage"
  instance_type = "t2.micro"
  min_size      = 2
  max_size      = 2
}
```



