# Terraform for Google Cloud

Terraform is an open source infrastructure as code (IaC) tool created by Hashicorp that lets provisioning cloud resources with declarative configuration files.
- Terraform supports all major cloud providers, in addition to google cloud and API-exposed services such as github and kubernetes.
- Terraform has an open source core structure.

## IaC configuration workflow
- Scope : confirm the resources required for a project.
- Author : Author the configuration files based on the scope.
- Initialize : Download the provider plugins and initialize directory.
- Plan : view execution plan for resources created. modified or destroyed.
- Apply : Create actual infrastucture resources.

## Terraform Directory
- Terraform uses configuration files to declare an infrastructure element.
- The configuration is written in terraform language with a **.tf** extension.
- A terraform directory can consist of multiple files and directories.
- A Configuration consist of :
  - a root module / root configuration
  - Zero or more child modules
  - Variable.tf (optional but recommended)
  - Outputs.tf (Optional but recommended)
- Terraform commands are run on the working directory.

## HashiCorp Configuration Language (HCL)
Syntax:
```
<BLOCK TYPE> "<BLOCK LABEL>" "<BLOCK LABEL>" {
  # Block body
  <IDENTIFIER> = <EXPRESSION> #Argument
}
```

### Resources
Resources are code blocks that define the infrastructure components.
A resource is identified by the keyword resource, followed by the resource type and a custom name.
The resource type depends on the provider defined in the configuration.

### Providers
Providers implement every resource type.
providers.tf file includes the provider definition.
Terraform downloads the provider plugin in the root configuration when the provider is declared.
Provider configuration belong in the root module of a terraform configuration.

### Variables
Variables are used to parametrize the configurations.
Once a variable is defined, there are various ways to set its values at runtime:
- environment variables
- CLI options
- key or value files .tfvars extension

### Outputs
outputs.tf holds output values from resources.
resource instances managed by terraform each export attributes whose values can be used elsewhere in configuration.

### State
Terraform saves the state of resources that it manages in a state file. By default the state file is stored locally, but it can also be stored remotely.


### Module
A Terraform module is a set of terraform configuration files in a single directory.
It is primary method for code reuse in terraform.
There are two kinds of sources - 
1. Local : source within directory
2. Remote : Source outside directory








