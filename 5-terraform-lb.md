# Terraform Task: Provision Two VMs with User Data and Load Balancer

## Overview

In this exercise, you will use Terraform to provision two virtual machine (VM) instances on a public cloud platform, attach a load balancer, and verify round-robin load balancing. The configuration should be cloud-neutral and adaptable to AWS, Azure, Google Cloud, or any other supported provider.

## Prerequisites

* Terraform installed and available in your `$PATH`.
* Credentials or environment variables configured for your target cloud provider (e.g., `AWS_ACCESS_KEY_ID`/`AWS_SECRET_ACCESS_KEY`, `AZURE_CLIENT_ID`/`AZURE_SECRET`, or `GOOGLE_CREDENTIALS`).
* Familiarity with Terraform provider blocks, resource definitions, count/for\_each meta-arguments, user data scripts, and load balancer configurations.
* A user data script file that performs simple initialization (e.g., installs a web server that returns the VM hostname).

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
3. **Write User Data Script**

   * Create a file (e.g., `init.sh` or `cloud-init.yaml`) containing commands to:

     * Install a simple web server.
     * Serve a page displaying the VM’s hostname or identifier.
4. **Define Variables**

   * In `variables.tf`, define:

     * `vm_count` (set default to 2)
     * `instance_type` or `size`
     * `image` or `image_id`
     * Network identifiers (e.g., VPC/subnet)
     * Load balancer settings (e.g., protocol, port)
5. **Create VM Resources**

   * In `main.tf`, add a VM resource block using `count`:

     ```hcl
     resource "<provider>_instance" "web" {
       count         = var.vm_count
       name          = "web-${count.index + 1}"
       instance_type = var.instance_type
       image_id      = var.image
       user_data     = file("./init.sh")
       # network settings...
     }
     ```
6. **Configure Load Balancer**

   * In `main.tf`, define a load balancer resource and attach the two VM instances:

     ```hcl
     resource "<provider>_load_balancer" "lb" {
       name               = "web-lb"
       protocol           = var.lb_protocol
       port               = var.lb_port
       target_instances   = <reference to instances>
       # other LB settings...
     }
     ```
7. **Plan and Apply**

   * Run:

     ```bash
     terraform plan
     terraform apply -auto-approve
     ```
   * Validate that two VMs and one load balancer are provisioned.
8. **Verify Round-Robin Load Balancing**

   * Send multiple HTTP requests to the load balancer’s address (e.g., `curl http://<LB_ADDRESS>`).
   * Observe alternating responses from each VM (hostname or identifier) to confirm round-robin distribution.

## Deliverables

* Terraform configuration files:

  * `main.tf` with provider, VM, and load balancer resources.
  * `variables.tf` defining inputs including `vm_count`, `instance_type`, `image`, and load balancer settings.
  * `outputs.tf` exposing the load balancer address and VM instance IDs or hostnames.
* A user data script file (`init.sh`, `cloud-init.yaml`, etc.).
* A file named `vm_lb_report.txt` containing:

  * The exact commands you executed (one per line).
  * The output of `terraform apply` confirming provisioning.
  * Evidence of user data execution (e.g., web server logs or page output).
  * Results of at least four `curl` requests showing round-robin responses.

---

**Note:** Do **not** include detailed solution explanations—only your configuration files, script, and command outputs as described.
