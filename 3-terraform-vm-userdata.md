# Terraform Task: Create a Virtual Machine with User Data

## Overview

In this exercise, you will use Terraform to provision a single virtual machine (VM) instance on a public cloud platform and supply custom initialization commands via user data. This cloud-neutral configuration can be adapted for AWS, Azure, Google Cloud, or any other supported provider.

## Prerequisites

* Terraform installed and available in your `$PATH`.
* Credentials or environment variables configured for your target cloud provider (e.g., `AWS_ACCESS_KEY_ID`/`AWS_SECRET_ACCESS_KEY`, `AZURE_CLIENT_ID`/`AZURE_SECRET`, or `GOOGLE_CREDENTIALS`).
* Basic understanding of Terraform provider blocks, resource definitions, and cloud-init or equivalent user data scripts.

## Task

1. **Set Up Project**

   * Create a new directory for your Terraform configuration and initialize it with `terraform init`.
2. **Define Provider**

   * Add a `provider` block with placeholder values:

     * `<PROVIDER_NAME>` (e.g., `aws`, `azurerm`, `google`)
     * `<REGION_OR_LOCATION>`
3. **Write User Data Script**

   * Create a plain-text file (e.g., `init.sh` or `cloud-init.yaml`) containing shell commands or cloud-init directives to run at first boot (e.g., install packages, configure services).
4. **Define VM Resource with User Data**

   * In `main.tf`, add a `resource` block for your VM instance, including:

     * `name` or `instance_name`
     * `instance_type` or `size`
     * `image` or `image_id`
     * Network settings (e.g., VPC/subnet, network interfaces)
     * `user_data` or `custom_data` argument referencing your script file:

       ```hcl
       user_data = file("./init.sh")
       ```
5. **Plan and Apply**

   * Run `terraform plan` to preview infrastructure changes.
   * Run `terraform apply -auto-approve` to provision the VM with your user data.
6. **Verify Initialization**

   * Connect to the VM (SSH or console) and confirm that the user data script executed correctly (e.g., packages installed, configurations applied).

## Deliverables

* Terraform configuration files (`main.tf`, plus any variables or modules) including:

  * A provider block with placeholders.
  * A VM resource block with user data integration.
* A user data script file (`init.sh`, `cloud-init.yaml`, etc.).
* A file named `vm_user_data_report.txt` documenting:

  * The exact commands you executed (one per line).
  * The output of `terraform apply` confirming VM creation.
  * Evidence that user data ran successfully (e.g., command outputs or log excerpts).

---

**Note:** Do **not** include the full solution in your report—only your configuration files, user data script, and command outputs as described.
