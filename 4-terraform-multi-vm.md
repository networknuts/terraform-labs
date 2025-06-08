# Terraform Task: Provision Multiple Virtual Machines

## Overview

In this exercise, you will use Terraform to provision multiple virtual machine (VM) instances on a public cloud platform. The configuration should be cloud-neutral and adaptable to AWS, Azure, Google Cloud, or any other supported provider.

## Prerequisites

* Terraform installed and available in your `$PATH`.
* Credentials or environment variables configured for your target cloud provider (e.g., `AWS_ACCESS_KEY_ID`/`AWS_SECRET_ACCESS_KEY`, `AZURE_CLIENT_ID`/`AZURE_SECRET`, or `GOOGLE_CREDENTIALS`).
* Familiarity with Terraform provider blocks, resource definitions, variables, and count or for\_each meta-arguments.

## Task

1. **Initialize Project**

   * Create a new directory for your Terraform configuration and initialize it with:

     ```bash
     terraform init
     ```
2. **Configure Provider**

   * Add a `provider` block in `main.tf` with placeholder values:

     ```hcl
     provider "<PROVIDER_NAME>" {
       region = "<REGION_OR_LOCATION>"
     }
     ```
3. **Define Variables**

   * Create a `variables.tf` file to accept:

     * `vm_count` (number of VMs to create)
     * `instance_type` or `size`
     * `image` or `image_id`
     * Any network identifiers (e.g., VPC/subnet)
4. **Create VM Resources**

   * In `main.tf`, add a VM resource block using `count` or `for_each`:

     ```hcl
     resource "<provider>_instance" "vm" {
       count         = var.vm_count
       name          = "vm-${count.index + 1}"
       instance_type = var.instance_type
       image_id      = var.image
       # network settings...
     }
     ```
5. **Plan and Apply**

   * Run:

     ```bash
     terraform plan
     terraform apply -auto-approve
     ```
   * Ensure Terraform provisions the specified number of VMs.
6. **Verify Instances**

   * Confirm VM instances are running via your cloud console or CLI.
   * Optionally, retrieve instance IDs or IP addresses:

     ```bash
     terraform output
     ```

## Deliverables

* Terraform configuration files:

  * `main.tf` with provider and resource definitions using `count` or `for_each`.
  * `variables.tf` defining input variables.
  * `outputs.tf` to expose instance IDs or addresses.
* A file named `multiple_vm_report.txt` containing:

  * The commands executed (one per line).
  * The output of `terraform apply` showing creation of each VM.
  * A list of created VM instance IDs or names.

---

**Note:** Do **not** include detailed solution explanations—only your configuration files and the command outputs as described.
