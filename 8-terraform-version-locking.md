# Terraform Task: Implement Version Locking

## Overview

In this exercise, you will configure Terraform to enforce provider and Terraform binary version constraints, ensuring consistent and repeatable infrastructure deployments across environments.

## Prerequisites

* Terraform installed and available in your `$PATH`.
* Familiarity with Terraform configuration syntax (`.tf` files).

## Task

1. **Initialize Project Structure**

   * Create a new directory for your Terraform configuration and run:

     ```bash
     terraform init
     ```
2. **Lock Terraform Binary Version**

   * In `versions.tf`, add a `required_version` block:

     ```hcl
     terraform {
       required_version = ">= 1.0.0, < 2.0.0"
     }
     ```
3. **Lock Provider Versions**

   * In the same file (`versions.tf`) or within `main.tf`, define `required_providers` blocks with version constraints:

     ```hcl
     terraform {
       required_providers {
         <provider_name> = {
           source  = "<namespace>/<provider>"
           version = ">= X.Y.Z, < X.Y+1.0"
         }
       }
     }
     ```
   * Replace `<provider_name>`, `<namespace>/<provider>`, and version numbers with placeholders.
4. **Verify Constraints**

   * Run:

     ```bash
     terraform init
     ```
   * Observe that Terraform enforces the specified versions or errors if mismatched.
5. **Test Version Mismatch**

   * Modify `required_version` or provider `version` constraints to incompatible values (e.g., `>= 9.0.0`), re-run `terraform init`, and record the error message.
6. **Document Findings**

   * Revert constraints to valid ranges and initialize again.

## Deliverables

* Configuration file `versions.tf` containing:

  * `required_version` constraint for the Terraform binary.
  * `required_providers` blocks with placeholder providers and version constraints.
* A file named `version_locking_report.txt` including:

  * The commands executed (`terraform init`) and their outputs.
  * Error output from the test mismatch.
  * Confirmation of successful initialization with correct constraints.

---

**Note:** Do **not** include any other resource definitions—only the version locking configuration and command outputs as described.
