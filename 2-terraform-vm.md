# Terraform Task: Create a Virtual Machine

## Overview

In this exercise, you will use Terraform to provision a single virtual machine (VM) instance on a public cloud platform. The goal is to create a cloud-neutral Terraform configuration that can be adapted to AWS, Azure, Google Cloud, or any other supported provider.

## Prerequisites

* Terraform installed and available in your `$PATH`.
* Credentials or environment variables configured for your target cloud provider (e.g., AWS\_ACCESS\_KEY\_ID/AWS\_SECRET\_ACCESS\_KEY, AZURE\_CLIENT\_ID/AZURE\_SECRET, or GOOGLE\_CREDENTIALS).
* Basic understanding of Terraform provider blocks and resource definitions.

## Task

1. **Initialize Directory**

   * Create a new directory for your Terraform configuration and run `terraform init`.
2. **Configure Provider**

   * Define a `provider` block with placeholder values:

     * `<PROVIDER_NAME>` (e.g., aws, azurerm, google)
     * `<REGION_OR_LOCATION>`
3. **Define VM Resource**

   * Create a `resource` block for a VM instance using generic arguments:

     * `name` or `instance_name`
     * `instance_type` or `size`
     * `image` or `image_id`
     * Network settings (e.g., VPC/subnet, network interfaces)
4. **Plan and Apply**

   * Run `terraform plan` to review changes.
   * Run `terraform apply -auto-approve` to provision the VM.
5. **Verify Deployment**

   * Confirm the VM is running in your cloud console or via CLI commands.

## Deliverables

* A Terraform configuration file (`main.tf`, plus any modules or variables files) containing:

  * A provider block with placeholders.
  * A resource block for a single VM instance.
* A file named `vm_creation_report.txt` including:

  * The exact commands you executed (one per line).
  * The output of `terraform apply` (successful creation messages).
  * The VM instance ID or name and region where it was created.

---

**Note:** Do **not** include the full solution in your report—only your configuration files and the command outputs as described.
