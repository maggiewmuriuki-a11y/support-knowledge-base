# 🎫 Service Desk Scenario: MFA Authentication Failure

**Ticket ID:** INC-20250312-004  
**Date Logged:** 12 March 2025  
**Priority:** High  
**Status:** ✅ Resolved  
**Category:** Identity & Access Management  
**Assigned To:** Margaret Muriuki, IT Support Specialist  
**SLA Breach:** No — Resolved within 4 hours  

---

## 🧾 Ticket Summary

**User:** James Omondi, Senior Finance Officer  
**Department:** Finance  
**Contact:** j.omondi@company.com | Ext. 204  
**Reported Via:** Phone → Logged in ServiceNow  

**User-Reported Issue:**  
> "I cannot log into my work account this morning. After entering my password, it asks for an MFA code but my authenticator app is not generating any codes."

---

## 🔍 Initial Assessment

**Gathered from user during intake call:**

- Issue started this morning after the user got a new phone over the weekend
- Old phone was reset/factory wiped — Microsoft Authenticator app was not backed up
- User confirmed password is correct but cannot complete the second authentication step
- User is working remotely and needs urgent access for a finance deadline at 11:00 AM

**Impact:**  
User is completely locked out of Microsoft 365, including Outlook, Teams, and the finance system. High-priority impact due to time-sensitive finance deadline.

---

## 🛠️ Investigation Steps

### Step 1: Verify User Identity
- Confirmed identity via employee ID and security question
- Verified with line manager (CFO) via phone that user is legitimate
- Checked Microsoft Entra ID admin center — account is active and in good standing

### Step 2: Check MFA Registration Status
- Navigated to: **Entra Admin Center → Users → [User] → Authentication Methods**
- Confirmed: Microsoft Authenticator is registered to the old device
- No backup phone number or email OTP was configured

### Step 3: Temporary Access Method
- Used admin privileges to enable a **Temporary Access Pass (TAP)** for the user
- Set TAP validity: **1 hour**, single use
- Sent TAP securely to user via Microsoft Teams (internal message, confirmed user is signed in on a secondary device)

### Step 4: MFA Re-Registration
Guided user through setting up Microsoft Authenticator on new phone:

1. User downloaded Microsoft Authenticator from App Store
2. Navigated to: `https://aka.ms/mfasetup`
3. Selected **"Add sign-in method" → Authenticator App**
4. Scanned QR code displayed on screen
5. Completed test authentication successfully

### Step 5: Verification
- Confirmed user can log in to Microsoft 365 with new MFA method
- Confirmed access to Outlook, Teams, and finance system restored
- Verified TAP has expired (single-use confirmed in Entra logs)

---

## ✅ Resolution

**Resolution Summary:**  
User's MFA was re-registered on their new device using a Temporary Access Pass (TAP). Full access to Microsoft 365 was restored within **3 hours and 42 minutes** of ticket creation — within SLA.

**Root Cause:**  
User replaced their phone without backing up the Microsoft Authenticator app and had no alternate authentication method configured.

---

## 📋 Actions Taken

| Action | Status |
|--------|--------|
| Identity verified | ✅ Complete |
| TAP issued | ✅ Complete |
| MFA re-registered on new device | ✅ Complete |
| User access confirmed | ✅ Complete |
| TAP expired and removed | ✅ Complete |
| Ticket closed in ServiceNow | ✅ Complete |

---

## 📌 Preventive Recommendations

1. **User Education:** Remind all staff to configure a backup MFA method (SMS or email OTP) in addition to the Authenticator app
2. **IT Policy:** Add MFA backup method as a requirement during user onboarding
3. **Comms:** Send a company-wide reminder before any planned device refresh/upgrade cycles

---

## 📝 Communication Log

| Time | Action |
|------|--------|
| 08:14 AM | Ticket received via phone, logged in ServiceNow |
| 08:20 AM | Called user back, gathered details |
| 08:35 AM | Identity verified with manager |
| 09:00 AM | TAP issued, user guided through MFA setup |
| 09:56 AM | Access confirmed, ticket resolved |
| 10:05 AM | Closure email sent to user |

---

## 📧 Closure Email Sent to User

> **Subject:** RE: INC-20250312-004 – MFA Issue Resolved  
>
> Hi James,  
>
> Your MFA has been successfully re-registered on your new device and your account access is fully restored.  
>
> As a recommendation, please consider adding a backup authentication method (such as a phone number for SMS codes) to avoid a similar issue in future. This can be done at: https://aka.ms/mfasetup  
>
> Please do not hesitate to reach out if you experience any further issues.  
>
> Kind regards,  
> Margaret Muriuki  
> IT Support Specialist  

---

*Ticket archived in ServiceNow under: Finance Department > INC-2025-March*
