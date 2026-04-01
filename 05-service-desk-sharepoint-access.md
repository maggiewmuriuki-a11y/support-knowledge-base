# 🎫 Service Desk Scenario: SharePoint Access Denied – Conditional Access Block

**Ticket ID:** INC-20250305-022  
**Date Logged:** 5 March 2025  
**Priority:** High  
**Status:** ✅ Resolved  
**Category:** Identity & Access Management — Conditional Access  
**Assigned To:** Margaret Muriuki, IT Support Specialist  
**SLA Breach:** No — Resolved within 3 hours  

---

## 🧾 Ticket Summary

**User:** David Njoroge, Operations Manager  
**Department:** Operations  
**Contact:** d.njoroge@company.com | Ext. 501  
**Reported Via:** Phone — escalated to ServiceNow  

**User-Reported Issue:**  
> "I am trying to access our SharePoint documents from my home laptop and I keep getting an error that says 'You don't have access to this content' or 'Your device does not meet compliance requirements.' I need to review an urgent operations report."

---

## 🔍 Initial Assessment

**Gathered from user during intake:**

- User is working remotely from home
- Using a **personal laptop** (not company-issued device)
- Was able to access SharePoint without issues last week
- New Conditional Access policies were rolled out by IT Security on 3 March 2025
- Error message: *"AADSTS53003: Access has been blocked by Conditional Access policies."*

**Impact:**  
User cannot access SharePoint documents. High priority — user needs to review and approve an operations report for a client-facing deadline.

---

## 🛠️ Investigation Steps

### Step 1: Verify User Identity & Account Status
- Identity confirmed via employee ID and manager verification
- Checked Entra ID: account is **Active**, no lockouts, MFA registered
- Sign-in logs reviewed in Entra: confirmed AADSTS53003 error at 08:47 AM

### Step 2: Review Sign-In Logs
- Navigated to: **Entra Admin Center → Sign-in Logs → Filter by User: David Njoroge**
- Error code: **AADSTS53003** — Blocked by Conditional Access
- Failure reason: **Device is not Entra ID Joined / Compliant**
- Applied policy: **"Require Compliant Device for SharePoint Access"** (enforced 3 March 2025)

### Step 3: Confirm Policy Scope
- Reviewed the new CA policy with IT Security team
- Confirmed: policy requires all SharePoint access from external devices to be:
  - **Entra ID Registered** or **Entra ID Joined**, AND
  - **Compliant** (meeting Intune device compliance requirements)
- User's personal laptop is **not enrolled** in Intune

### Step 4: Identify Immediate Workaround
Two options presented to user and manager:

**Option A (Short-term):** Access SharePoint via **company-issued laptop**  
→ User confirmed they have a company laptop at home — had been using personal laptop for convenience

**Option B (Short-term):** Enable **Web Browser-Only access** exception  
→ Discussed with IT Security — approved for 24-hour exception window via Named Location policy adjustment

**Decision made:** User to switch to company laptop (Option A) — faster and more secure.

### Step 5: Confirm Access on Company Device
- User switched to company-issued laptop
- Confirmed device is Entra ID Joined and compliant in Intune
- Tested SharePoint access — **successful**
- Confirmed access to the operations report folder

### Step 6: Long-Term Recommendation
Discussed with IT Security and documented recommendation for personal device enrollment option for remote staff.

---

## ✅ Resolution

**Resolution Summary:**  
User was guided to use their company-issued laptop, which is enrolled and compliant. Access to SharePoint was confirmed within **2 hours 51 minutes**. The root cause was a new Conditional Access policy that blocks non-compliant devices.

**Root Cause:**  
A new Conditional Access policy (enforced 3 March 2025) requires compliant, Entra ID-enrolled devices for SharePoint access. The user's personal laptop did not meet these requirements.

---

## 📋 Actions Taken

| Action | Status |
|--------|--------|
| Identity and account status verified | ✅ Complete |
| Sign-in logs reviewed in Entra ID | ✅ Complete |
| CA policy confirmed with IT Security | ✅ Complete |
| User switched to company device | ✅ Complete |
| SharePoint access confirmed | ✅ Complete |
| Long-term recommendations documented | ✅ Complete |
| Ticket closed in ServiceNow | ✅ Complete |

---

## 📌 Preventive Recommendations

1. **Communication Gap:** The new CA policy rollout on 3 March 2025 was not communicated to end users. Recommend a company-wide notice before any future policy changes affecting access.
2. **Personal Device Enrollment:** Create a process for remote employees to optionally enroll personal devices via Intune for compliant access.
3. **Self-Service Guidance:** Add a knowledge base article on this error to the ServiceNow employee portal so users can self-diagnose.
4. **Manager Awareness:** Brief department managers on the new policy so they can advise their teams.

---

## 📝 Communication Log

| Time | Action |
|------|--------|
| 08:52 AM | Ticket raised via phone; logged in ServiceNow |
| 09:00 AM | User called back; details gathered |
| 09:15 AM | Sign-in logs reviewed; root cause identified |
| 09:30 AM | Confirmed policy details with IT Security |
| 10:05 AM | User guided to use company laptop |
| 11:43 AM | Access confirmed; ticket resolved |
| 11:55 AM | Closure email sent |

---

## 📧 Closure Email Sent to User

> **Subject:** RE: INC-20250305-022 – SharePoint Access Restored  
>
> Hi David,  
>
> Your SharePoint access has been fully restored on your company-issued device.  
>
> To clarify what happened: our IT Security team rolled out a new security policy on 3 March that requires all devices accessing SharePoint to be enrolled and compliant with company standards. Personal devices do not currently meet this requirement.  
>
> Going forward, please use your company laptop for SharePoint access when working remotely. If you would like to enrol your personal device as an alternative, please raise a new request and we can guide you through the process.  
>
> Apologies for any inconvenience caused. Please do not hesitate to get in touch if you need anything further.  
>
> Kind regards,  
> Margaret Muriuki  
> IT Support Specialist  

---

## 🔗 Related Articles

- [Microsoft: AADSTS53003 Error Code Reference](https://learn.microsoft.com/en-us/azure/active-directory/develop/reference-error-codes)
- [How to Enrol a Device in Microsoft Intune](#)
- [Company Remote Work Device Policy](#)

---

*Ticket archived in ServiceNow under: Operations Department > INC-2025-March*
