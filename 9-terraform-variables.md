# Terraform Task: Use Variables in Configuration

## Overview

In this exercise, you will refactor a basic Terraform configuration to use input variables, making it more flexible and reusable across environments and deployments. This cloud-neutral setup works with any public cloud provider.

## Prerequisites

* Terraform installed and available in your `$PATH`.
* A simple Terraform configuration (`main.tf`) that defines at least one resource (e.g., a VM instance).
* Familiarity with Terraform variable syntax and CLI commands.

## Task

1. **Initialize Project**

   * Ensure you have a Terraform configuration directory and run:

     ```bash
     terraform init
     ```
2. **Create Variables File**

   * In your project directory, create a `variables.tf` file.
   * Define input variables for parameters such as:

     * `region` (cloud region or location)
     * `instance_type` or `size`
     * `image_id` or `image`
     * Any tags, names, or counts you want to parameterize.
   * Use sensible defaults where appropriate and include descriptions:

     ```hcl
     variable "region" {
       description = "The cloud region to deploy resources in"
       type        = string
       default     = "<REGION_OR_LOCATION>"
     }

     variable "instance_type" {
       description = "VM instance type or size"
       type        = string
       default     = "<INSTANCE_TYPE>"
     }
     ```
3. **Reference Variables in Configuration**

   * In `main.tf`, replace hardcoded values with variable references:

     ```hcl
     provider "<provider>" {
       region = var.region
     }

     resource "<provider>_instance" "vm" {
       name          = "example-vm"
       instance_type = var.instance_type
       image_id      = var.image_id
       # additional resource settings...
     }
     ```
4. **Create a Terraform.tfvars File**

   * Create a `terraform.tfvars` file to override defaults for a specific environment:

     ```hcl
     region        = "us-west-2"
     instance_type = "t3.small"
     image_id      = "ami-0abcdef1234567890"
     ```
5. **Plan and Apply with Variables**

   * Run a plan to confirm variable values are applied:

     ```bash
     terraform plan
     ```
   * Apply the configuration using the `.tfvars` file implicitly or explicitly:

     ```bash
     terraform apply -var-file="terraform.tfvars" -auto-approve
     ```
6. **Override Variables at the CLI**

   * Demonstrate overriding a variable without editing files:

     ```bash
     terraform apply -var="instance_type=t3.medium" -auto-approve
     ```
7. **Output Variable Values**

   * In `outputs.tf`, define outputs that use variables or resource attributes:

     ```hcl
     output "vm_id" {
       description = "ID of the created VM"
       value       = <reference to resource.id>
     }

     output "deployed_region" {
       description = "Region where VM is deployed"
       value       = var.region
     }
     ```
   * Run:

     ```bash
     terraform output
     ```
   * Confirm outputs display expected values.

## Deliverables

* Terraform configuration files:

  * `main.tf` updated to reference variables.
  * `variables.tf` defining all input variables.
  * `terraform.tfvars` providing environment-specific values.
  * `outputs.tf` with at least two outputs including one that echoes a variable.
* A file named `variable_usage_report.txt` containing:

  * The commands you ran (e.g., `terraform init`, `terraform plan`, `terraform apply` with flags).
  * The output of `terraform apply` showing variable values in use.
  * The output of `terraform output` displaying the configured outputs.

---

**Note:** Do **not** include provider credentials or detailed provider-specific settings—only generic variable usage and resource references as described.
