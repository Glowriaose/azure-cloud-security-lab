# Fabrikam Financial Services : Azure Secure Cloud Environment

**Project ID:** `FAB-SEC-001`  
**Role:** Cloud Security Engineer (Capstone/Lab Project)  
**Platform:** Microsoft Azure  

---

## About the Project

This project simulates a financial services scenario where sensitive workloads demand strict data protection, least-privilege access controls, and defense-in-depth networking. 

Throughout the build, I configured and integrated **Microsoft Entra ID groups**, **Azure RBAC**, **system-assigned managed identities**, **Azure Key Vault**, **private endpoints with private DNS zones**, **Azure Policy**, and **Log Analytics monitoring**. Rather than just scripting a happy path, I deliberately troubleshot deployment roadblocks such as fine tuning role assignments and resolving network boundaries to ensure a production-grade security posture.

---

## Project Documentation

* **[Part 1: Identity and Access Management](../01-identity-acces/01-identity-and-access-management.md)**  
  Organizing access to Key Vault using Microsoft Entra ID groups and Azure RBAC, configuring the VM's system-assigned managed identity, testing secret retrieval, and cleaning up broad administrative permissions during troubleshooting.
* **[Part 2: Azure Resources, Networking and RBAC](../02-azure-networking-rbac/02-azure-networking-and-rbac.md)**  
  A breakdown of the resource topology (Resource Group, VNet, subnets, Ubuntu 24.04 VM, Key Vault, Private Endpoint, and Private DNS), detailing how network isolation and access permissions intersect.
* **[Part 3: Monitoring, Governance and Handover](../03-monitoring-governance/03-monitoring-governance.md)**  
  Enforcing compliance via Azure Policy, configuring Microsoft Defender for Cloud, wiring up Log Analytics workspaces, and setting up operational security alerts.

---

## Key Implementation Decisions

* **Compute Selection:** I originally planned to deploy via Azure App Service, but hit subscription quota constraints when attempting to provision App Service instances in the `East US` region. Rather than blocking deployment, I pivoted to an Ubuntu 24.04 virtual machine (`vm-fab-sec-001`). This allowed me to continue testing and gave direct, low-level CLI visibility into system-assigned managed identities and secret retrieval mechanics.
* **Granular RBAC Strategy:** I enforced strict separation of duties using Azure RBAC. The VM's workload identity is restricted to the **Key Vault Secrets User** role. Any broader administrative permissions temporarily granted during initial debugging were systematically revoked.
* **Defense-in-Depth (Network vs. Identity):** Emphasized that a private endpoint only secures the transit path, while RBAC governs authorization. Both layers must be configured independently and correctly having network reachability does not bypass identity permissions, and vice versa.

---

## Architecture & Evidence

* **Architecture Diagram:** [View Architecture Diagram](architecture/fabrikam-financial-services-architecture.svg) *
* **Implementation Artifacts:** The `evidence/` directory contains sanitized screenshots capturing resource configurations, IAM policies, and monitoring logs. 
  > *Note: Secret values, subscription IDs, tenant IDs, object IDs, and internal IP addresses have been redacted from all public screenshots.*

---

## What I Learned

Working on this project helped me understand how different Azure security controls work together. I had to troubleshoot managed identity access, resolve private DNS issues, and configure Azure Policy to enforce security requirements. When things didn’t work as expected, I made adjustments and tested different approaches. This helped me understand the importance of getting identity, network access, and permissions right when securing resources in Azure.

***

*This is a lab project based on a Client financial services environment, built to develop and demonstrate core Azure cloud security and infrastructure engineering skills.*