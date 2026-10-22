# Entra ID Access Review (P2)

Hands-on lab, October 2026 (done Oct 19).

## What this is and why it matters

An access review checks access people **already have** and removes what they no longer need. I ran a one-time review of the group **MFA-Test-Group** in Microsoft Entra ID P2. **Test User** was a member but hadn't signed in for 30+ days, so I denied continued access with a reason, and Entra removed them automatically. The group went from **1 member to 0**.

This is how companies keep access clean for audits: someone accountable confirms each person still needs access, and the removal is applied and logged, not done by hand. It rechecks access people already have. Requests for *new* access are a separate flow (approval / dual control, like in my CyberArk lab).

## Environment

| Item | Value |
| --- | --- |
| Tenant | Entra ID lab tenant with **Microsoft Entra ID P2** (needed for access reviews) |
| Review | **Q4 MFA-Test-Group** (Teams + Groups, scope: All users) |
| Reviewer | Lab Admin |
| Duration / recurrence | 3 days, one time, start 10/19/2026 |
| Member reviewed | Test User |

## Steps

### 1. Confirm the P2 license

![P2 license](screenshots/01-p2-license-status.png)

### 2. Identity Governance → Access reviews

![Access reviews page](screenshots/02-access-reviews-page.png)

### 3. Review type: Teams + Groups → MFA-Test-Group, All users

![Review type](screenshots/03-review-type.png)

### 4. Reviewer: Lab Admin, 3 days, one time

![Reviewers](screenshots/04-reviewers.png)

### 5. Settings

- Auto apply results to resource: **on**
- If reviewers don't respond: **No change**
- Decision helper: **No sign-in within 30 days**
- Justification required, email notifications and reminders: **on**

![Settings](screenshots/05-settings.png)

### 6. Review created, then active

![Review created](screenshots/06-review-created.png)
![Review active](screenshots/08-review-active.png)

### 7. Before: MFA-Test-Group has 1 member (Test User)

![Group before](screenshots/07-mfa-test-group-members-before.png)

### 8. Reviewer decision in My Access: Deny, with a reason

Entra recommended **Deny** because Test User was inactive. I denied with the reason: *"Test account, no longer needs MFA testing access."*

![Deny with reason](screenshots/09-deny-with-reason.png)
![Reviewer completed](screenshots/10-reviewer-completed.png)

### 9. Stop the review → Complete, 1 denied

I stopped the review once the decision was in. **Apply** is grayed out because auto-apply was on, so Entra applied the deny by itself.

![Review stopped](screenshots/11-review-stopped.png)
![Review complete: 1 denied](screenshots/12-review-complete-1-denied.png)

### 10. After: MFA-Test-Group has 0 members

![Group after: 0 members](screenshots/13-group-0-members-after.png)

## What I got wrong at first, and fixed

At first I described this as denying someone who *requests* access. That's not what an access review is. It reviews access people **already have**. New requests go through an approval workflow instead. I corrected my understanding during the lab.

## Skills shown

- **IAM Support:** running a group access review, documenting a deny with justification, confirming removal
- **IAM Engineer / Identity Governance:** configuring Entra ID P2 access reviews (scope, reviewers, auto-apply, decision helpers)
- **PAM / least privilege:** removing inactive access automatically, audit-ready evidence
- Knowing the difference between access reviews (recertification) and access requests (approval)

## Notes

- Blacked out in screenshots: object IDs, review/tenant IDs in the browser URL, and the tenant name (account email and user names).
- Lab tenant and test accounts only; no real user data.
