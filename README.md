# Automated Network Change Request Management in ServiceNow

> A ServiceNow-based workflow automation solution for managing network change requests, approvals, fulfillment tasks, and email notifications through a structured and automated process.

---

## Project Overview

The **Automated Network Change Request Management System** is a ServiceNow application designed to streamline the process of submitting, reviewing, approving, and fulfilling network-related change requests.

The system provides a centralized Service Catalog interface where users can submit network requests such as:

- VLAN Change
- Firewall Rule
- IP Allocation
- VPN Access

Once a request is submitted, the system automatically routes it to the appropriate approval group. Based on the approval decision, the request is either:

- Approved → Fulfillment task is created and the request is completed.
- Rejected → The request is marked as incomplete.
- Approval notifications are automatically sent to the assigned approver.

The project demonstrates how ServiceNow can be used to automate an end-to-end enterprise request management process.

---

## Project Objectives

The main objectives of this project are:

1. Automate network change request submission.
2. Standardize network request information through Service Catalog variables.
3. Implement role-based access and group-based approvals.
4. Automate approval workflows using Workflow Studio.
5. Automatically create fulfillment tasks after approval.
6. Send email notifications to approvers and requesters.
7. Maintain request and approval status throughout the lifecycle.
8. Provide a scalable and maintainable ServiceNow solution.
9. Package configurations using ServiceNow Update Sets.
10. Maintain project documentation and deployment artifacts in GitHub.

---

## System Architecture

```text
                         ┌──────────────────────┐
                         │      End User        │
                         └──────────┬───────────┘
                                    │
                                    ▼
                    ┌─────────────────────────────┐
                    │     Service Catalog         │
                    │  Network Change Request     │
                    └─────────────┬───────────────┘
                                  │
                                  ▼
                    ┌─────────────────────────────┐
                    │       Requested Item         │
                    │          RITM                │
                    └─────────────┬───────────────┘
                                  │
                                  ▼
                    ┌─────────────────────────────┐
                    │      Workflow Studio        │
                    │ Network Change Request      │
                    │          Approval           │
                    └─────────────┬───────────────┘
                                  │
                         ┌────────┴────────┐
                         │                 │
                         ▼                 ▼
                    ┌──────────┐      ┌──────────┐
                    │ Approved │      │ Rejected │
                    └────┬─────┘      └────┬─────┘
                         │                 │
                         ▼                 ▼
              ┌──────────────────┐   ┌──────────────────┐
              │ Create Catalog   │   │ Closed Incomplete│
              │      Task        │   └──────────────────┘
              └────────┬─────────┘
                       │
                       ▼
              ┌──────────────────┐
              │   Network Team   │
              │    Fulfillment   │
              └────────┬─────────┘
                       │
                       ▼
              ┌──────────────────┐
              │ Closed Complete  │
              └──────────────────┘
