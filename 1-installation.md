# Terraform Installation on RHEL

## Overview

In this exercise, you will install Terraform on a Red Hat Enterprise Linux (RHEL) system. Terraform is an open-source Infrastructure as Code tool by HashiCorp.

## Prerequisites

* A RHEL 7, 8, or 9 instance with at least 2 GB of RAM.
* A user account with sudo privileges.
* Internet connectivity or access to HashiCorp download mirrors.

## Task

Follow these steps to complete the installation:

1. **Check RHEL Version**

   * Determine the OS version by inspecting `/etc/redhat-release`.
2. **Install Dependencies**

   * Identify and install any packages required for running Terraform (e.g., `unzip`, `curl` or `wget`).
3. **Download Terraform**

   * Fetch the official Terraform binary for Linux from HashiCorp’s releases.
4. **Verify Checksum**

   * Validate the integrity of the downloaded archive using the SHA256 checksum provided by HashiCorp.
5. **Unpack and Install**

   * Unzip the Terraform binary and move it to a system-wide location (e.g., `/usr/local/bin`).
6. **Configure Permissions**

   * Ensure the Terraform binary is executable and available on the system `$PATH`.
7. **Validate Installation**

   * Run `terraform version` to confirm the installed version.
8. **Document Outcomes**

   * Note any errors or warnings encountered during the process.

## Deliverables

* A file named `installation_report.txt` containing:

  * The exact commands you executed (one per line).
  * The output of `terraform version`.
  * Any error messages or troubleshooting notes, if applicable.

---

**Note:** Do **not** include detailed explanations in your report—only the commands and their outputs.
