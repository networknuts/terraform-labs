# Terraform Task: Terraform Cloud and Sentinel Policies

## Overview

In this exercise, you will configure Terraform to use Terraform Cloud for state management and apply Sentinel policies to enforce governance rules. The configuration should be cloud-neutral and applicable to any public cloud provider.

## Prerequisites

* Terraform CLI installed and available in your `$PATH`.
* A Terraform Cloud organization and workspace created (or permissions to create one).
* Terraform Cloud API token configured (e.g., via `TFC_TOKEN` environment variable).
* Familiarity with Terraform configuration syntax and basic Sentinel policy language.

## Task

1. **Initialize Terraform Cloud Backend**

   * In your Terraform configuration directory, create or update `backend.tf` to configure Terraform Cloud:

     ```hcl
     terraform {
       backend "remote" {
         hostname     = "app.terraform.io"
         organization = "<YOUR_ORG>"

         workspaces {
           name = "<WORKSPACE_NAME>"
         }
       }
     }
     ```
   * Run:

     ```bash
     terraform init
     ```
   * Confirm that Terraform Cloud is set as the backend.

2. **Push Configuration to VCS (Optional)**

   * If using VCS-driven runs, push your Terraform files to a connected repository and trigger a run in Terraform Cloud.

3. **Create Sentinel Policy Files**

   * In a `sentinel/` directory, create at least two policy files:

     * **policy\_require\_tags.sentinel**: Enforce that all resources have a `tags` or equivalent attribute defined.
     * **policy\_restrict\_regions.sentinel**: Restrict resource creation to approved regions only.
   * Each policy should include placeholder logic:

     ```python
     # Example structure
     import "tfplan/v2" as tfplan

     main = rule {
       all tfplan.resources as _, instances {
         instances.appearance.count > 0 implies has_tags(instances)
       }
     }

     has_tags = func(instances) {
       # Placeholder for tag check
       true
     }
     ```

4. **Upload Sentinel Policies to Terraform Cloud**

   * In Terraform Cloud UI, navigate to Policies, create a new policy set, and upload your `sentinel/` policies.

5. **Trigger a Terraform Run**

   * From the CLI or VCS, initiate a Terraform plan/apply in the configured workspace:

     ```bash
     terraform plan
     terraform apply -auto-approve
     ```
   * Observe that Sentinel policies are evaluated before apply.

6. **Validate Policy Enforcement**

   * Deliberately violate a policy (e.g., remove tags from a resource or specify an unapproved region) and rerun:

     ```bash
     terraform plan
     ```
   * Capture the Sentinel policy failure messages.

## Deliverables

* Terraform configuration files:

  * `backend.tf` configuring Terraform Cloud remote backend.
  * Any `.tf` files defining resources (e.g., a simple VM or network).
* Sentinel policy files in `sentinel/`:

  * `policy_require_tags.sentinel`
  * `policy_restrict_regions.sentinel`
* A file named `sentinel_report.txt` containing:

  * The commands you executed (`terraform init`, `terraform plan`, `terraform apply`).
  * Evidence of successful runs with policies passing.
  * Examples of policy failures and their messages.

---

**Note:** Do **not** include actual policy logic—use placeholders and document outcomes as described.
