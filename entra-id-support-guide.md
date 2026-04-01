# Microsoft Entra ID: Support and Troubleshooting Guide

**Document Type:** Knowledge Base Article  
**Category:** Identity and Access Management  
**Applies To:** End Users | IT Support Staff  
**Last Updated:** March 2025  
**Author:** IT Application Support

---

## Overview

Microsoft Entra ID (formerly Azure Active Directory) is the identity and access management platform used across the organization. It controls user authentication, application access, multi-factor authentication (MFA), and device compliance. This guide covers the most common issues encountered by end users and the steps support staff should follow to resolve them.

---

## Table of Contents

1. [User Cannot Sign In](#1-user-cannot-sign-in)
2. [MFA Issues](#2-mfa-issues)
3. [Account Locked or Disabled](#3-account-locked-or-disabled)
4. [User Provisioning](#4-user-provisioning)
5. [User Deprovisioning](#5-user-deprovisioning)
6. [Guest and External User Access](#6-guest-and-external-user-access)
7. [Conditional Access Blocks](#7-conditional-access-blocks)
8. [Password Reset](#8-password-reset)
9. [Escalation Guidance](#9-escalation-guidance)

---

## 1. User Cannot Sign In

### Symptoms
- Error: *"Your account or password is incorrect"*
- Error: *"This account has been locked"*
- Redirect loop at the sign-in page
- Sign-in page does not load

### Resolution Steps

**Step 1 — Verify the username format**  
Ensure the user is signing in with their full organizational email address (e.g., `firstname.lastname@organization.org`). Personal email addresses will not work.

**Step 2 — Check account status in Entra ID**  
1. Open the Microsoft Entra admin center (entra.microsoft.com)
2. Go to Users > All Users
3. Search for the user by name or email
4. Check that the account is enabled (Account enabled = Yes)
5. Review the sign-in logs for the last failed attempt (Users > Sign-in logs)

**Step 3 — Check for sign-in errors in logs**  
Common error codes and their meanings:

| Error Code | Meaning | Action |
|---|---|---|
| AADSTS50126 | Invalid username or password | Reset password |
| AADSTS50057 | Account disabled | Re-enable account |
| AADSTS50053 | Account locked due to too many failed attempts | Unlock account |
| AADSTS50076 | MFA required but not completed | Assist with MFA |
| AADSTS530003 | Device not compliant | Check Intune compliance |

**Step 4 — Clear browser cache and cookies**  
Ask the user to clear their browser cache or try signing in using a private/incognito window.

**Step 5 — Try a different browser or device**  
This helps isolate whether the issue is device or browser-specific.

---

## 2. MFA Issues

### 2a. User Did Not Receive MFA Code

**Possible Causes**
- Incorrect phone number registered
- Mobile network delay
- Authenticator app not synced

**Resolution Steps**
1. Ask the user to wait 60 seconds and request the code again
2. If using SMS, verify the registered phone number in Entra ID:
   - Go to Users > Select user > Authentication methods
   - Confirm the phone number on file is correct
3. If using the Microsoft Authenticator app, ask the user to open the app and check if a push notification is pending
4. If the app is not responding, ask the user to tap the refresh icon in the Authenticator app
5. As a temporary measure, switch the user to SMS if Authenticator is not working

### 2b. User Lost Access to MFA Device (Lost or New Phone)

**Resolution Steps**
1. Verify the user's identity through an alternative channel (manager confirmation, staff ID)
2. Navigate to Users > Select user > Authentication methods
3. Delete the existing MFA methods (phone number and/or Authenticator app)
4. Ask the user to re-register MFA at aka.ms/mfasetup
5. Document the incident in ServiceNow with the verification method used

### 2c. User Locked Out Completely (No MFA Access)

Escalate to the Identity and Access Management team. Do not bypass MFA without completing identity verification. Refer to the escalation section below.

---

## 3. Account Locked or Disabled

### Account Locked (Too Many Failed Sign-in Attempts)

1. Go to Entra admin center > Users > All Users
2. Search for and select the user
3. Under Account status, check if the account shows as locked
4. Click Unlock account
5. Advise the user to reset their password before attempting to sign in again

### Account Disabled (Intentionally or by Policy)

1. Confirm with the user's line manager or HR that re-enabling is authorized
2. Go to Users > Select user > Edit properties
3. Toggle Account enabled to Yes
4. Save changes
5. Notify the user and log the action in ServiceNow with manager authorization noted

---

## 4. User Provisioning

Use this process when onboarding a new staff member or creating a new account.

### Pre-Requisites
- Completed onboarding request form approved by HR
- Line manager confirmation of role, department, and required access
- Start date confirmed

### Steps

1. **Create the user account**
   - Go to Entra admin center > Users > New user > Create new user
   - Fill in: Display name, Username, First name, Last name, Job title, Department

2. **Assign a license**
   - Go to the user profile > Licenses > Assignments
   - Assign the appropriate Microsoft 365 license based on role

3. **Add to security groups**
   - Add the user to the relevant department and application security groups
   - This determines which applications and resources the user can access

4. **Configure MFA**
   - MFA is enforced by policy and will prompt the user on first sign-in
   - Share the MFA setup link with the user: aka.ms/mfasetup

5. **Send welcome communication**
   - Provide the user with their username, temporary password, and MFA setup instructions
   - Direct them to the IT onboarding guide

6. **Log in ServiceNow**
   - Record the provisioning request number, approver, and date completed

---

## 5. User Deprovisioning

Use this process when a staff member exits the organization.

### Steps

1. **Disable the account immediately on last working day**
   - Go to Users > Select user > Edit properties
   - Set Account enabled to No

2. **Revoke active sessions**
   - On the user profile page, click Revoke sessions
   - This signs the user out of all active Microsoft 365 sessions immediately

3. **Remove licenses**
   - Go to Licenses > Assignments and remove all assigned licenses

4. **Transfer mailbox and OneDrive access**
   - Follow the offboarding checklist to assign mailbox delegate access to the line manager
   - Grant OneDrive access to the manager for a minimum of 30 days

5. **Remove from security groups**
   - Remove the user from all department and application groups

6. **Schedule account deletion**
   - Accounts are permanently deleted 30 days after disabling unless a retention hold is requested by HR or Legal

7. **Log in ServiceNow**
   - Record completion against the offboarding ticket, including confirmation of session revocation and license removal

---

## 6. Guest and External User Access

### Inviting an External User

1. Go to Entra admin center > Users > New user > Invite external user
2. Enter the external user's email address and a personal message
3. Assign them only to the specific SharePoint site, Teams channel, or application they need
4. Set an access expiry date where possible (recommended: 90 days)
5. Notify the internal team member who requested the access

### Removing External User Access

1. Go to Users > All Users > filter by User type = Guest
2. Select the guest user
3. Remove them from all groups and application assignments
4. Delete the guest account

---

## 7. Conditional Access Blocks

### Symptoms
- User receives error: *"You cannot access this resource from your current location or device"*
- Access blocked when connecting from a new country
- Access blocked on a personal or unmanaged device

### Resolution Steps

1. Check the sign-in logs for the specific conditional access policy that triggered the block
   - Go to Users > Sign-in logs > Select the failed event > Conditional Access tab
2. Identify whether the block is due to:
   - **Location** — user is in an unlisted country (check if travel was expected)
   - **Device compliance** — device not enrolled in Intune or not meeting compliance policy
   - **Application policy** — specific app requires managed device or approved client app
3. If the block is due to travel:
   - Verify with the user and their manager
   - Raise a temporary named location exception with the IAM team if authorized
4. If the block is due to device compliance:
   - Direct the user to enroll their device in Intune
   - Refer to the Intune Device Enrollment Quick Reference Guide

Do not disable or modify conditional access policies without approval from the IAM team lead.

---

## 8. Password Reset

### Self-Service Password Reset (SSPR)

Users can reset their own password at passwordreset.microsoftonline.com provided they have registered for SSPR. Direct users here before raising a support ticket.

### Admin Password Reset

1. Go to Entra admin center > Users > Select user
2. Click Reset password
3. Choose to auto-generate or set a temporary password
4. Require the user to change password on next sign-in (recommended)
5. Communicate the temporary password to the user through a secure channel (not email)

---

## 9. Escalation Guidance

Escalate to the IAM team or senior application support in the following situations:

| Situation | Escalation Path |
|---|---|
| Complete lockout with no MFA recovery options | IAM Team Lead |
| Bulk provisioning or deprovisioning (10+ accounts) | IAM Team Lead |
| Conditional access policy modification request | IAM Team Lead + Security |
| Suspicious sign-in activity or potential account compromise | Security Operations + IAM |
| Entra ID service outage | Check Microsoft Service Health Dashboard first, then escalate to IAM |
| Guest access governance review | Business Relationship Manager |

When escalating, always include:
- The affected user's full name and email address
- The ServiceNow ticket number
- A summary of steps already taken
- Any relevant error codes from the sign-in logs

---

## Related Documents

- MFA Setup Quick Reference Guide
- Microsoft 365 Onboarding Guide
- Intune Device Enrollment Quick Reference Guide
- Offboarding Checklist
- ServiceNow Incident Logging Guide

---

*This document is intended for internal IT support use. Do not share externally. For updates or corrections contact the IT Application Support team.*
