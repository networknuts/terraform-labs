# Terraform Task: Create and Manage Multiple Workspaces

## Overview

In this exercise, you will use Terraform to create and manage multiple workspaces in a cloud-neutral configuration. Workspaces allow you to maintain separate state files—for example, `dev`, `staging`, and `prod`—within the same configuration directory.

## Prerequisites

* Terraform installed and available in your `$PATH`.
* A basic Terraform configuration (`main.tf`, etc.) initialized in your project directory.
* Familiarity with Terraform CLI and state management concepts.

## Task

1. **Initialize Project**

   * Ensure you have a Terraform configuration directory and run:

     ```bash
     terraform init
     ```
2. **List Default Workspace**

   * Verify the default workspace by running:

     ```bash
     terraform workspace list
     ```
3. **Create Additional Workspaces**

   * Create at least two new workspaces (e.g., `dev` and `prod`):

     ```bash
     terraform workspace new dev
     terraform workspace new prod
     ```
4. **Switch Between Workspaces**

   * Select each workspace in turn and observe the workspace context:

     ```bash
     terraform workspace select dev
     terraform workspace select prod
     ```
5. **Apply Configuration per Workspace**

   * In each workspace, run `terraform plan` and `terraform apply -auto-approve` to provision resources scoped to that workspace.
   * Note: Use the same configuration but separate state files per workspace.
6. **List and Show Current Workspace**

   * List all workspaces again and show the current active one:

     ```bash
     terraform workspace list
     terraform workspace show
     ```
7. **Delete a Workspace**

   * Delete one of the custom workspaces (e.g., `dev`) after destroying its resources:

     ```bash
     terraform destroy -auto-approve
     terraform workspace select default
     terraform workspace delete dev
     ```

## Deliverables

* A short `workspace_tasks.txt` file containing:

  * The exact Terraform CLI commands you ran (one per line).
  * The output of `terraform workspace list` after creating and after deleting workspaces.
* A brief log excerpt showing `terraform workspace show` to confirm workspace context.

---

**Note:** Do **not** include the full Terraform configuration or resource definitions in your deliverables—only the CLI commands and their outputs as described.
