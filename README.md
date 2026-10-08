# AZ-104 — Azure Subscriptions and RBAC

## Overview

This project demonstrates Azure governance and Role-Based Access Control
(RBAC) using Microsoft Azure.

The lab focuses on organizing Azure subscriptions with management groups,
assigning built-in Azure roles to groups, creating a custom RBAC role based
on the principle of least privilege, and monitoring role assignments using
the Azure Activity Log.

## Scenario

An organization wants to simplify the management of its Azure environment
and provide controlled access to its subscriptions.

A Help Desk team requires the ability to manage virtual machines and
submit support requests, while unnecessary permissions should be
restricted.

To achieve this, a management group is created to organize subscriptions,
RBAC permissions are assigned to a Help Desk group, and a custom support
role is created with unnecessary permissions removed.

## Objectives

- Create an Azure management group
- Understand management group hierarchy
- Review built-in Azure RBAC roles
- Assign the Virtual Machine Contributor role
- Assign permissions to a security group instead of an individual
- Create a custom RBAC role
- Apply the principle of least privilege
- Exclude unnecessary permissions from a custom role
- Review RBAC role definitions
- Monitor role assignments using Activity Log

## Technologies

- Microsoft Azure
- Azure Management Groups
- Azure RBAC
- Azure Access Control (IAM)
- Microsoft Entra ID
- Azure Activity Log
- Azure Portal

## Architecture

![Azure RBAC Architecture](diagrams/architecture.png)


# Implementation

## 1. Create the Management Group

Created a management group named:

`az104-mg1`

The management group provides a higher-level scope for organizing Azure
subscriptions and applying access control.

![Management Group](screenshots/01-management-group.png)

**Result:** The `az104-mg1` management group was successfully created.


## 2. Create the Help Desk Security Group

Created a Microsoft Entra ID security group named:

`helpdesk`

The group is used as the identity to which the Azure RBAC role will be
assigned.

![Help Desk Group](screenshots/02-helpdesk-group.png)

**Result:** The Help Desk security group was successfully created.


## 3. Review Azure RBAC Roles

Reviewed the built-in Azure role definitions available through the
Access Control (IAM) interface.

Azure provides built-in roles with predefined permissions that can be
assigned at different scopes.

![RBAC Roles](screenshots/03-rbac-roles.png)

**Result:** Reviewed available built-in roles and their permissions.


## 4. Assign the Virtual Machine Contributor Role

Assigned the **Virtual Machine Contributor** role to the `helpdesk`
security group at the `az104-mg1` management group scope.

The Virtual Machine Contributor role allows the Help Desk to manage
virtual machines without granting permissions to access the operating
system or manage the associated virtual network and storage account.

![Virtual Machine Contributor Assignment](screenshots/04-vm-contributor-assignment.png)

**Result:** The `helpdesk` group was assigned the Virtual Machine
Contributor role.


## 5. Verify the Role Assignment

Reviewed the Role assignments section of Access Control (IAM) to verify
that the `helpdesk` group had the expected role assignment.

![Role Assignment Verification](screenshots/05-role-assignment-verification.png)

**Result:** The `helpdesk` group was successfully listed with the
Virtual Machine Contributor role.


## 6. Create a Custom RBAC Role

Created a custom role named:

`Custom Support Request`

Description:

`A custom contributor role for support requests.`

The custom role was based on the existing **Support Request Contributor**
role.

![Custom Role](screenshots/06-custom-role.png)

**Result:** A custom RBAC role was configured based on an existing
built-in role.

## 7. Exclude Unnecessary Permissions

The custom role was modified to exclude the permission:

`Microsoft.Support/register/action`

This permission allows registration of the Microsoft.Support resource
provider.

The permission was excluded because the Help Desk does not require the
ability to register the support resource provider.

![Excluded Permission](screenshots/07-excluded-permission.png)

**Result:** The unnecessary permission was excluded from the custom role.


## 8. Review the Custom Role JSON

Reviewed the JSON definition of the custom RBAC role.

The definition contains elements such as:

- Actions
- NotActions
- AssignableScopes

![Custom Role JSON](screenshots/08-custom-role-json.png)

**Result:** Reviewed how Azure represents custom RBAC roles using JSON.


## 9. Monitor Role Assignments

Used the Azure Activity Log to monitor role assignment activity within the
management group.

The Activity Log provides visibility into administrative operations
performed within the Azure environment.

![Activity Log](screenshots/09-activity-log.png)

**Result:** Role assignment activity was reviewed using the Activity Log.


# Security Considerations

## Principle of Least Privilege

The custom role demonstrates the principle of least privilege by removing
permissions that are not required for the Help Desk's responsibilities.

Users and groups should only receive the permissions necessary to perform
their assigned tasks.

## Group-Based Access

The RBAC role was assigned to the `helpdesk` group rather than directly
to an individual user.

Group-based role assignments simplify administration and make it easier
to manage permissions when team membership changes.

## Scope

The role assignment was applied at the management group level.

This allows permissions to be inherited by resources within the relevant
scope while avoiding the need to configure the same assignment
individually across multiple subscriptions.

## Monitoring

The Azure Activity Log provides visibility into role assignment
operations and can help administrators monitor changes to access
permissions.


# RBAC Concepts Demonstrated

### Management Groups

Management groups provide a way to logically organize Azure subscriptions
and provide a higher-level scope for governance and access control.

### Role-Based Access Control

Azure RBAC controls what actions identities can perform and at which
scope those permissions apply.

### Built-in Roles

Azure provides predefined roles such as Reader, Contributor, Owner and
Virtual Machine Contributor.

### Custom Roles

Custom roles can be created when built-in roles provide more permissions
than required for a particular job function.

### Scope

Azure role assignments can be applied at different scopes, allowing
administrators to control where permissions are effective.

### Actions and NotActions

Custom role definitions can specify permitted actions and exclude
unnecessary actions.


# Troubleshooting

Document any issues encountered during the lab here.

Example:

### Authorization Error

**Problem:** An authorization error was encountered when accessing the
management group's IAM configuration.

**Investigation:** The Azure portal session credentials were refreshed.

**Resolution:** Signed out of Azure Portal and signed back in before
continuing with the role assignment.


# What I Learned

- How Azure management groups can organize subscriptions.
- How Azure RBAC controls access to Azure resources.
- Why roles should generally be assigned to groups rather than individual
  users.
- How built-in roles can provide predefined permissions.
- When custom roles may be appropriate.
- How the principle of least privilege can be implemented using custom
  roles.
- How Activity Log can be used to monitor role assignment activity.
- How custom Azure RBAC roles are represented using JSON.


# Skills Demonstrated

### Azure Administration

- Azure Management Groups
- Azure Portal
- Access Control (IAM)
- Subscription governance

### Identity & Access Management

- Microsoft Entra ID
- Security Groups
- Group-based access
- Role assignments

### Azure RBAC

- Built-in roles
- Custom roles
- Role scopes
- Actions
- NotActions
- AssignableScopes

### Security

- Least privilege
- Access governance
- Permission management
- Activity monitoring


# Future Improvements

Potential extensions to this project include:

- Automating management group creation with Azure CLI
- Automating RBAC assignments using PowerShell
- Creating RBAC roles using JSON
- Exploring Azure Policy
- Implementing Privileged Identity Management
- Testing different RBAC scopes
- Automating role-assignment monitoring


**Certification Track:** Microsoft AZ-104 — Azure Administrator

**Focus Areas:** Governance, RBAC, Identity & Access Management
