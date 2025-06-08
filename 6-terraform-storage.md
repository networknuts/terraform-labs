# Terraform Task: Provision a VM with Additional Block Device Storage

## Overview

In this exercise, you will use Terraform to provision a single virtual machine (VM) instance on a public cloud platform and attach an additional block storage device. The configuration should be cloud-neutral and adaptable to AWS, Azure, Google Cloud, or any other supported provider.

## Prerequisites

* Terraform installed and available in your `$PATH`.
* Credentials or environment variables configured for your target cloud provider (e.g., `AWS_ACCESS_KEY_ID`/`AWS_SECRET_ACCESS_KEY`, `AZURE_CLIENT_ID`/`AZURE_SECRET`, or `GOOGLE_CREDENTIALS`).
* Familiarity with Terraform provider blocks, resource definitions, and block storage attachment concepts.

## Task

1. **Initialize Project**

   * Create a new directory for your Terraform configuration and run:

     ```bash
     terraform init
     ```
2. **Configure Provider**

   * In `main.tf`, add a `provider` block with placeholders:

     ```hcl
     provider "<PROVIDER_NAME>" {
       region = "<REGION_OR_LOCATION>"
     }
     ```
3. **Define Variables**

   * In `variables.tf`, define input variables for:

     * VM instance attributes (e.g., `instance_type`, `image_id`).
     * Block device settings:

       * `volume_size` (in GB)
       * `volume_type` or `storage_account_type`
       * Any tags or identifiers.
     * Network identifiers (e.g., VPC/subnet).
4. **Create VM Resource**

   * In `main.tf`, add a VM resource block:

     ```hcl
     resource "<provider>_instance" "vm" {
       name          = "example-vm"
       instance_type = var.instance_type
       image_id      = var.image_id
       # network settings...
     }
     ```
5. **Attach Block Storage Device**

   * Still in `main.tf`, add a block device resource or nested block within the VM resource:

     ```hcl
     resource "<provider>_volume" "data" {
       size             = var.volume_size
       type             = var.volume_type
       # additional volume params...
     }

     resource "<provider>_volume_attachment" "attach" {
       instance_id = <reference to vm id>
       volume_id   = <reference to data volume id>
       device_name = "/dev/sdb"
     }
     ```
6. **Plan and Apply**

   * Run:

     ```bash
     terraform plan
     terraform apply -auto-approve
     ```
   * Ensure Terraform provisions the VM and attaches the additional block device.
7. **Verify Attachment**

   * Connect to the VM (SSH or console).
   * List block devices (e.g., `lsblk` on Linux) to confirm the attached volume appears and is available.

## Deliverables

* Terraform configuration files:

  * `main.tf` with provider, VM, and block device resources.
  * `variables.tf` defining VM and storage inputs.
  * `outputs.tf` exposing the VM ID and volume ID.
* A file named `vm_storage_report.txt` containing:

  * The exact commands you executed (one per line).
  * The output of `terraform apply` confirming resource creation.
  * Output from the VM verifying the block device (e.g., `lsblk`).

---

**Note:** Do **not** include detailed solution explanations—only your configuration files and the command outputs as described.
