# 🎫 Service Desk Scenario: Account Lockout After Failed Login Attempts

**Ticket ID:** INC-20250219-011  
**Date Logged:** 19 February 2025  
**Priority:** Medium  
**Status:** ✅ Resolved  
**Category:** Identity & Access Management — Account Lockout  
**Assigned To:** Margaret Muriuki, IT Support Specialist  
**SLA Breach:** No — Resolved within 2 hours  

---

## 🧾 Ticket Summary

**User:** Lydia Kamau, HR Coordinator  
**Department:** Human Resources  
**Contact:** l.kamau@company.com | Ext. 318  
**Reported Via:** ServiceNow Self-Service Portal  

**User-Reported Issue:**  
> "I have been locked out of my account. I tried logging in several times this morning and now I get a message saying my account has been locked. I have an important HR meeting in 2 hours."

---

## 🔍 Initial Assessment

**Gathered from user during callback:**

- User returned from annual leave (1 week off)
- Attempted to log in multiple times with what she believed was her current password
- After 5 failed attempts, the account was locked by the system (standard security policy)
- User is unsure if her password expired while she was on leave

**Impact:**  
User locked out of Microsoft 365 (Outlook, Teams, HR system). Medium priority — HR meeting in 2 hours creates time sensitivity.

---

## 🛠️ Investigation Steps

### Step 1: Verify Identity
- User verified via employee ID number (HR-0087) and date of birth
- Cross-checked details in Entra ID admin center — confirmed legitimate user account

### Step 2: Check Account Status in Entra ID
- Navigated to: **Entra Admin Center → Users → Lydia Kamau**
- Account status: **Locked** (due to failed sign-in attempts)
- Last successful login: 10 February 2025 (before leave)
- Password last changed: 11 November 2024
- Password expiry policy: 90 days
- **Finding:** Password had expired on 11 February 2025 while user was on leave

### Step 3: Unlock the Account
- Clicked **"Unlock Account"** in Entra Admin Center
- Account status confirmed as Active

### Step 4: Trigger Password Reset
- Selected **"Reset Password"** and enabled **"Require user to change password on next login"**
- Sent temporary password to user's personal email address (confirmed with user)

### Step 5: Guide User Through Password Change
Provided step-by-step instructions:
1. Go to `https://portal.office.com`
2. Enter username and temporary password
3. When prompted, create a new password meeting policy requirements:
   - Minimum 12 characters
   - At least 1 uppercase, 1 lowercase, 1 number, 1 special character
   - Cannot reuse last 5 passwords
4. Complete MFA verification
5. Confirm access to Outlook and Teams

### Step 6: Confirm Resolution
- User confirmed successful login at 10:42 AM
- Verified access to Outlook, Teams, and HR system
- Account status in Entra ID: **Active, no lockout flags**

---

## ✅ Resolution

**Resolution Summary:**  
Account was unlocked in Entra ID and a forced password reset was issued. User successfully updated her password and regained full access within **1 hour 38 minutes** — within SLA.

**Root Cause:**  
User's password expired during annual leave. On return, she attempted login with the expired password multiple times, triggering the automatic account lockout (policy: lock after 5 failed attempts).

---

## 📋 Actions Taken

| Action | Status |
|--------|--------|
| Identity verified | ✅ Complete |
| Account unlocked in Entra ID | ✅ Complete |
| Password reset triggered | ✅ Complete |
| User guided through new password creation | ✅ Complete |
| Access to all systems confirmed | ✅ Complete |
| Ticket closed in ServiceNow | ✅ Complete |

---

## 📌 Preventive Recommendations

1. **Password Expiry Notifications:** Ensure users receive email reminders at 14, 7, and 3 days before password expiry
2. **Leave Management Coordination:** HR to flag employees returning from extended leave so IT can proactively check account status
3. **Self-Service Password Reset (SSPR):** Confirm SSPR is enabled for all users so minor lockouts can be self-resolved without a ticket
4. **User Education:** Include a reminder about password expiry in the "Return from Leave" HR checklist

---

## 📝 Communication Log

| Time | Action |
|------|--------|
| 09:04 AM | Ticket submitted by user via portal |
| 09:15 AM | Ticket picked up; called user |
| 09:20 AM | Identity verified; investigation started |
| 09:35 AM | Account unlocked; password reset triggered |
| 09:40 AM | User guided through password change |
| 10:42 AM | User confirmed access restored |
| 10:50 AM | Ticket closed; closure email sent |

---

## 📧 Closure Email Sent to User

> **Subject:** RE: INC-20250219-011 – Account Access Restored  
>
> Hi Lydia,  
>
> Your account has been successfully unlocked and your password has been reset. You should now have full access to all your systems.  
>
> Going forward, you'll receive reminder emails before your password is due to expire. If you're ever locked out again, you can also use the self-service password reset at: https://aka.ms/sspr  
>
> I hope your HR meeting went well. Please reach out if you need anything further.  
>
> Kind regards,  
> Margaret Muriuki  
> IT Support Specialist  

---

*Ticket archived in ServiceNow under: HR Department > INC-2025-February*
