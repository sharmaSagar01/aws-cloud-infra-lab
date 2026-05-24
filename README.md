# ☁️ AWS Cloud Infrastructure Lab

> Builds a production-style cloud infrastructure on **Amazon Web Services**
> using the AWS Free Tier — covering networking, compute, storage, monitoring,
> and security across both Windows and Linux environments.
> Extends the existing on-premises `InfoTech.com` homelab into a second cloud platform,
> making the environment truly hybrid and cloud-agnostic.

<div align="center">

![AWS](https://img.shields.io/badge/Amazon_AWS-Free_Tier-FF9900?style=flat-square&logo=amazonaws)
![EC2](https://img.shields.io/badge/EC2-Compute-FF9900?style=flat-square&logo=amazonec2)
![VPC](https://img.shields.io/badge/VPC-Networking-FF9900?style=flat-square)
![S3](https://img.shields.io/badge/S3-Storage-FF9900?style=flat-square&logo=amazons3)
![IAM](https://img.shields.io/badge/IAM-Identity-FF9900?style=flat-square)
![Status](https://img.shields.io/badge/Status-In%20Progress-yellow?style=flat-square)

</div>

---

## 📌 Overview

AWS is the most widely used cloud platform in the Canadian job market.
This project builds a complete cloud infrastructure environment from scratch —
covering the core AWS services that appear in every IT, sysadmin, and
cloud support role: identity, networking, compute, storage, and monitoring.

**What this project demonstrates:**

- Designing and deploying a custom VPC with public and private subnets
- Launching and managing Windows Server and Linux EC2 instances
- Configuring IAM users, groups, roles, and least-privilege policies
- Managing S3 storage with bucket policies, versioning, and lifecycle rules
- Setting up CloudWatch monitoring with alarms and log groups
- Hardening the AWS environment following security best practices

---

## 🏗️ Architecture

```
┌──────────────────────────────────────────────────────────────────┐
│                        AWS Cloud (Free Tier)                     │
│                                                                  │
│   ┌──────────────────────────────────────────────────────────┐  │
│   │                  Custom VPC (10.0.0.0/16)                │  │
│   │                                                          │  │
│   │   ┌─────────────────┐    ┌─────────────────┐            │  │
│   │   │  Public Subnet  │    │  Private Subnet  │            │  │
│   │   │  10.0.1.0/24   │    │  10.0.2.0/24    │            │  │
│   │   │                 │    │                  │            │  │
│   │   │  EC2 Windows    │    │  EC2 Linux       │            │  │
│   │   │  (RDP port 3389)│    │  (SSH port 22)   │            │  │
│   │   └────────┬────────┘    └─────────┬────────┘            │  │
│   │            │                       │                      │  │
│   │   Internet Gateway          NAT Gateway                   │  │
│   └────────────┼───────────────────────┼──────────────────────┘  │
│                │                       │                         │
│   ┌────────────▼───────────────────────▼──────────────────────┐  │
│   │                    Other AWS Services                      │  │
│   │    S3 Buckets    CloudWatch    IAM    Security Hub         │  │
│   └────────────────────────────────────────────────────────────┘  │
└──────────────────────────────────────────────────────────────────┘
                              │
                    (Future Phase — VPN)
                              │
┌─────────────────────────────▼────────────────────────────────────┐
│               On-Premises Lab (VMware)                           │
│   VM-WINSERV-01 (192.168.1.10)   VM-WINSERV-02 (192.168.1.12)  │
│   InfoTech.com Active Directory — synced to Entra ID            │
└──────────────────────────────────────────────────────────────────┘
```

---

## 🖥️ Environment

<table>
<tr>
<td width="50%" valign="top">

**AWS**
| Component | Details |
|-----------|---------|
| **Account** | AWS Free Tier |
| **Region** | ca-central-1 (Canada) |
| **VPC** | Custom — `10.0.0.0/16` |
| **Public Subnet** | `10.0.1.0/24` |
| **Private Subnet** | `10.0.2.0/24` |
| **EC2 (Windows)** | `t2.micro` — Windows Server 2022 |
| **EC2 (Linux)** | `t2.micro` — Ubuntu 22.04 |

</td>
<td width="50%" valign="top">

**On-Premises (Reference)**
| Component | Details |
|-----------|---------|
| **Primary DC** | `VM-WINSERV-01` — `192.168.1.10` |
| **Secondary DC** | `VM-WINSERV-02` — `192.168.1.12` |
| **Domain** | `InfoTech.com` |
| **Azure Tenant** | `yourtenant.onmicrosoft.com` |

</td>
</tr>
</table>

---

## 📁 Repository Structure

```
aws-cloud-infra-lab/
│
├── config/
│   ├── iam-config.md          # IAM users, groups, roles, policies     ✅
│   ├── vpc-config.md          # VPC, subnets, route tables, SGs        ✅
│   ├── ec2-config.md          # EC2 instances and configuration         ⏳
│   ├── s3-config.md           # S3 buckets, policies, lifecycle         ⏳
│   └── cloudwatch-config.md   # Monitoring, alarms, log groups          ⏳
│
├── screenshots/
│   └── (phase screenshots added as project progresses)
│
├── docs/
│   └── runbook.md             # Operational runbook                     ⏳
│
└── README.md
```

> ⏳ = In progress — added as the project develops

---

## 🧩 Build Progress

| #   | Phase                                                                 | Status       |
| --- | --------------------------------------------------------------------- | ------------ |
| 1   | AWS Free Tier setup + IAM users, groups, and MFA                      | ✅ Completed |
| 2   | Custom VPC — subnets, route tables, security groups, internet gateway | ✅ Completed |
| 3   | EC2 — launch Windows and Linux instances, connect via RDP and SSH     | ⏳ Pending   |
| 4   | S3 — buckets, policies, versioning, and lifecycle rules               | ⏳ Pending   |
| 5   | CloudWatch — monitoring, alarms, dashboards, and log groups           | ⏳ Pending   |
| 6   | IAM hardening + AWS security best practices                           | ⏳ Pending   |
| 7   | Runbook + final documentation + GitHub push                           | ⏳ Pending   |

---

## 🎯 What You Will Have at the End

| Capability           | Details                                                            |
| -------------------- | ------------------------------------------------------------------ |
| **Cloud Networking** | Custom VPC with public and private subnets                         |
| **Compute**          | Windows Server and Ubuntu EC2 instances                            |
| **Identity**         | IAM users, groups, roles, and least-privilege policies             |
| **Storage**          | S3 buckets with policies, versioning, and lifecycle management     |
| **Monitoring**       | CloudWatch dashboards, alarms, and log groups                      |
| **Security**         | MFA on root, least-privilege IAM, security groups, hardened config |

---

## ⚙️ Prerequisites

**AWS Free Tier includes (sufficient for this project):**

| Service       | Free Tier Limit                  |
| ------------- | -------------------------------- |
| EC2           | 750 hours/month — `t2.micro`     |
| S3            | 5 GB storage                     |
| CloudWatch    | 10 custom metrics, 5 GB log data |
| IAM           | Always free                      |
| VPC           | Always free                      |
| Data Transfer | 100 GB out/month                 |

> ⚠️ **Important:** Always check the AWS Free Tier usage dashboard
> before running instances. Stop EC2 instances when not in use to
> avoid unexpected charges.
> Set a billing alert at $5 immediately after account creation.

**Before starting Phase 1:**

- Sign up at `https://aws.amazon.com/free`
- A valid credit card is required for identity verification
- You will not be charged within Free Tier limits
- Select **Canada (Central) — ca-central-1** as your default region

---

# ✅ Phase 1 — AWS Account Setup, IAM & Billing

## 📋 What This Phase Covers

Before touching any AWS service, the account needs to be secured and
structured properly. This phase locks down the root account, creates
a dedicated admin user following AWS best practice, sets up IAM groups
and policies, and configures billing alerts to protect against unexpected charges.

> Full IAM configuration reference: [`config/iam-config.md`](config/iam-config.md)

---

## ⚙️ Part A — Secure the Root Account

The root account has unrestricted access to everything in AWS.
Best practice is to secure it immediately and never use it for day-to-day work.

**Step 1 — Enable MFA on Root**

```
AWS Console → click your account name (top right)
→ Security credentials
→ Multi-factor authentication (MFA)
→ Assign MFA device
→ Select: Authenticator app
→ Scan QR code with Microsoft Authenticator or Google Authenticator
→ Enter two consecutive codes to verify → Add MFA
```

**Step 2 — Remove Root Access Keys (if any exist)**

```
Security credentials → Access keys
→ If any keys exist → Delete them
→ Root should never have programmatic access keys
```

---

## ⚙️ Part B — Set a Billing Alert

Do this before creating any resources — takes 2 minutes and
protects against unexpected charges.

```
AWS Console → search "Billing"
→ Budgets → Create budget
→ Use a template: Zero spend budget
   OR
→ Monthly cost budget → set amount: $10
→ Alert threshold: 80% of budget
→ Email: your email address
→ Create budget
```

Also enable billing alerts via CloudWatch:

```
Billing → Billing preferences
→ Check: Receive CloudWatch Billing Alerts → Save
```

---

## ⚙️ Part C — Set Default Region to Canada

```
AWS Console → top right region selector
→ Select: Canada (Central) — ca-central-1
```

All resources created in this project use `ca-central-1` unless
stated otherwise.

---

## ⚙️ Part D — Create an IAM Admin User

Never use the root account for daily work. Create a dedicated
IAM admin user instead:

```
AWS Console → search "IAM" → Users → Create user
```

| Field                      | Value                 |
| -------------------------- | --------------------- |
| **Username**               | `iamadmin`            |
| **Console access**         | Yes                   |
| **Password**               | Set a strong password |
| **Require password reset** | No                    |

**Attach permissions:**

```
Attach policies directly
→ Search: AdministratorAccess
→ Check it → Next → Create user
```

**Save the sign-in URL:**

```
IAM → Dashboard → AWS Account section
→ Copy the sign-in URL:
  https://YOUR-ACCOUNT-ID.signin.aws.amazon.com/console
```

Sign out of root → sign back in as `iamadmin` using the IAM sign-in URL.
Use this account for all remaining phases.

---

## ⚙️ Part E — Enable MFA on the IAM Admin User

```
IAM → Users → iamadmin
→ Security credentials tab
→ Multi-factor authentication → Assign MFA device
→ Authenticator app → scan QR → verify → Add MFA
```

Sign out and sign back in — confirm MFA is prompted on login ✅

---

## ⚙️ Part F — Create IAM Groups and Users

Structure IAM with groups so permissions are managed at the group
level — not assigned individually to users:

**Create Groups:**

```
IAM → User groups → Create group
```

| Group Name   | Policy Attached     | Purpose              |
| ------------ | ------------------- | -------------------- |
| `Admins`     | AdministratorAccess | Full admin access    |
| `Developers` | PowerUserAccess     | All except IAM       |
| `ReadOnly`   | ReadOnlyAccess      | View only — auditing |

**Create Lab Users:**

```
IAM → Users → Create user
```

| Username        | Group      | Purpose                               |
| --------------- | ---------- | ------------------------------------- |
| `iamadmin`      | Admins     | Primary admin — used for all lab work |
| `dev-user`      | Developers | Simulates a developer account         |
| `readonly-user` | ReadOnly   | Simulates an auditor account          |

---

## ⚙️ Part G — Create a Custom IAM Policy

Practice writing a custom IAM policy — this is a real-world skill
tested in interviews. Create a policy that allows S3 read-only access
to a specific bucket:

```
IAM → Policies → Create policy → JSON tab
```

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "S3ReadOnlySpecificBucket",
      "Effect": "Allow",
      "Action": ["s3:GetObject", "s3:ListBucket"],
      "Resource": [
        "arn:aws:s3:::infotech-lab-bucket",
        "arn:aws:s3:::infotech-lab-bucket/*"
      ]
    }
  ]
}
```

| Field           | Value                                   |
| --------------- | --------------------------------------- |
| **Policy Name** | `S3ReadOnly-InfoTechBucket`             |
| **Description** | Read-only access to infotech-lab-bucket |

---

## ⚙️ Part H — Explore the IAM Security Dashboard

```
IAM → Security recommendations
```

All items should be green after completing this phase:

| Check                      | Expected Status |
| -------------------------- | --------------- |
| Root MFA enabled           | ✅ Green        |
| Root access keys deleted   | ✅ Green        |
| IAM admin user created     | ✅ Green        |
| Admin user MFA enabled     | ✅ Green        |
| Password policy configured | ✅ Green        |

**Set a password policy:**

```
IAM → Account settings → Password policy → Edit
→ Minimum length: 12
→ Require uppercase: Yes
→ Require numbers: Yes
→ Require symbols: Yes
→ Save changes
```

---

## ✅ Outcome

- Root account secured — MFA enabled, access keys removed ✅
- Billing alert configured — $10 budget with email notification ✅
- Default region set to `ca-central-1` (Canada Central) ✅
- IAM admin user `iamadmin` created with AdministratorAccess ✅
- MFA enabled on `iamadmin` — root never used again ✅
- 3 IAM groups created — Admins, Developers, ReadOnly ✅
- 3 IAM users created and assigned to groups ✅
- Custom IAM policy written in JSON — S3 read-only ✅
- IAM Security Dashboard — all checks green ✅

---

## 📸 Screenshots

<p align="center">
  <img src="screenshots/phase1/phase1-img1.png" width="45%"
        />
  <img src="screenshots/phase1/phase1-img2.png" width="45%"
        />
</p>
<p align="center">
  <img src="screenshots/phase1/phase1-img3.png" width="45%"
       />
  <img src="screenshots/phase1/phase1-img4.png" width="45%"
        />
</p>

<p align="center">
  <img src="screenshots/phase1/phase1-img5.png" width="45%"
       />
  <img src="screenshots/phase1/phase1-img6.png" width="45%"
        />
</p>
---

---
 
# ✅ Phase 2 — Custom VPC & Networking
 
## 📋 What This Phase Covers
 
The VPC (Virtual Private Cloud) is the networking foundation for everything
built in AWS. This phase builds a custom VPC from scratch — public and private
subnets, internet gateway, route tables, NAT gateway, and security groups.
Every EC2 instance, S3 endpoint, and CloudWatch resource in later phases
lives inside this VPC.
 
> Full VPC configuration reference: [`config/vpc-config.md`](config/vpc-config.md)
 
---
 
## 🔍 VPC Architecture
 
```
VPC: 10.0.0.0/16
│
├── Public Subnet (10.0.1.0/24) — ca-central-1a
│   ├── Internet Gateway attached
│   ├── Route: 0.0.0.0/0 → Internet Gateway
│   └── EC2 Windows Server (Phase 3)
│
└── Private Subnet (10.0.2.0/24) — ca-central-1b
    ├── No direct internet access
    ├── Route: 0.0.0.0/0 → NAT Gateway
    └── EC2 Linux Ubuntu (Phase 3)
```
 
---
 
## ⚙️ Part A — Create the Custom VPC
 
```
AWS Console → search "VPC" → Your VPCs → Create VPC
```
 
| Field | Value |
|-------|-------|
| **Resources to create** | VPC only |
| **Name tag** | `InfoTech-VPC` |
| **IPv4 CIDR** | `10.0.0.0/16` |
| **IPv6** | No IPv6 CIDR block |
| **Tenancy** | Default |
 
Click **Create VPC** ✅
 
---
 
## ⚙️ Part B — Create Subnets
 
Create two subnets — one public, one private — in different
availability zones for high availability.
 
```
VPC → Subnets → Create subnet
→ Select VPC: InfoTech-VPC
```
 
**Public Subnet:**
 
| Field | Value |
|-------|-------|
| **Subnet name** | `InfoTech-Public-Subnet` |
| **Availability Zone** | `ca-central-1a` |
| **IPv4 CIDR** | `10.0.1.0/24` |
 
**Private Subnet:**
 
| Field | Value |
|-------|-------|
| **Subnet name** | `InfoTech-Private-Subnet` |
| **Availability Zone** | `ca-central-1b` |
| **IPv4 CIDR** | `10.0.2.0/24` |
 
**Enable auto-assign public IP on the public subnet:**
```
Subnets → select InfoTech-Public-Subnet
→ Actions → Edit subnet settings
→ Enable auto-assign public IPv4 address → Save
```
 
---
 
## ⚙️ Part C — Create and Attach Internet Gateway
 
The Internet Gateway (IGW) allows resources in the public subnet
to communicate with the internet.
 
```
VPC → Internet gateways → Create internet gateway
```
 
| Field | Value |
|-------|-------|
| **Name tag** | `InfoTech-IGW` |
 
Click **Create** → then **Attach to VPC** → select `InfoTech-VPC` ✅
 
---
 
## ⚙️ Part D — Create Route Tables
 
Route tables control where traffic flows from each subnet.
 
**Public Route Table:**
 
```
VPC → Route tables → Create route table
```
 
| Field | Value |
|-------|-------|
| **Name** | `InfoTech-Public-RT` |
| **VPC** | `InfoTech-VPC` |
 
Add a route to send all internet traffic to the IGW:
```
Select InfoTech-Public-RT → Routes tab → Edit routes → Add route
Destination: 0.0.0.0/0
Target: InfoTech-IGW
Save changes
```
 
Associate with the public subnet:
```
Subnet associations tab → Edit subnet associations
→ Select: InfoTech-Public-Subnet → Save
```
 
**Private Route Table:**
 
```
Create route table
Name: InfoTech-Private-RT
VPC: InfoTech-VPC
```
 
Associate with the private subnet:
```
Subnet associations → Edit → Select: InfoTech-Private-Subnet → Save
```
 
> The private route table has no internet route by default.
> Traffic from private subnet goes through the NAT Gateway (Part E).
 
---
 
## ⚙️ Part E — Create NAT Gateway
 
The NAT Gateway allows instances in the private subnet to reach
the internet for updates — without exposing them to inbound traffic.
 
```
VPC → NAT gateways → Create NAT gateway
```
 
| Field | Value |
|-------|-------|
| **Name** | `InfoTech-NAT-GW` |
| **Subnet** | `InfoTech-Public-Subnet` (NAT must be in public subnet) |
| **Connectivity type** | Public |
| **Elastic IP** | Allocate Elastic IP → click Allocate |
 
Click **Create NAT gateway** — takes 1–2 minutes to become Available.
 
Once available, add the NAT route to the private route table:
```
Route tables → InfoTech-Private-RT → Routes → Edit routes → Add route
Destination: 0.0.0.0/0
Target: InfoTech-NAT-GW
Save changes
```
 
> ⚠️ **Cost note:** NAT Gateway charges approximately $0.045/hour.
> Delete it when not in use — recreate when needed.
> For Free Tier labs, stop the NAT Gateway between sessions.
 
---
 
## ⚙️ Part F — Create Security Groups
 
Security Groups act as virtual firewalls controlling inbound and
outbound traffic at the instance level.
 
**Security Group 1 — Windows EC2 (RDP access)**
 
```
VPC → Security groups → Create security group
```
 
| Field | Value |
|-------|-------|
| **Name** | `InfoTech-Windows-SG` |
| **VPC** | `InfoTech-VPC` |
 
Inbound rules:
 
| Type | Protocol | Port | Source | Purpose |
|------|----------|------|--------|---------|
| RDP | TCP | 3389 | My IP | Remote desktop access |
| ICMP | All | All | 10.0.0.0/16 | Internal ping |
 
Outbound rules: Allow all (default) ✅
 
---
 
**Security Group 2 — Linux EC2 (SSH access)**
 
| Field | Value |
|-------|-------|
| **Name** | `InfoTech-Linux-SG` |
| **VPC** | `InfoTech-VPC` |
 
Inbound rules:
 
| Type | Protocol | Port | Source | Purpose |
|------|----------|------|--------|---------|
| SSH | TCP | 22 | My IP | SSH access |
| ICMP | All | All | 10.0.0.0/16 | Internal ping |
 
Outbound rules: Allow all (default) ✅
 
---
 
## ⚙️ Part G — Enable VPC Flow Logs
 
VPC Flow Logs capture all network traffic in and out of the VPC —
useful for security monitoring and troubleshooting.
 
```
VPC → Your VPCs → select InfoTech-VPC
→ Flow logs tab → Create flow log
```
 
| Field | Value |
|-------|-------|
| **Filter** | All |
| **Destination** | CloudWatch Logs |
| **Log group** | `/aws/vpc/infotech-flow-logs` (create new) |
| **IAM role** | Create new role — allow VPC to write to CloudWatch |
 
---
 
## ✅ Outcome
 
- Custom VPC `InfoTech-VPC` created — `10.0.0.0/16` ✅
- Public subnet `10.0.1.0/24` in `ca-central-1a` ✅
- Private subnet `10.0.2.0/24` in `ca-central-1b` ✅
- Internet Gateway created and attached to VPC ✅
- Public route table — routes internet traffic via IGW ✅
- Private route table — routes outbound traffic via NAT Gateway ✅
- NAT Gateway created in public subnet ✅
- Security Group for Windows EC2 — RDP on port 3389 ✅
- Security Group for Linux EC2 — SSH on port 22 ✅
- VPC Flow Logs enabled — sending to CloudWatch ✅
---
<p align="center">
  <img src="screenshots/phase2/phase2-img1.png" width="45%"
        />
  <img src="screenshots/phase2/phase2-img2.png" width="45%"
        />
</p>
<p align="center">
  <img src="screenshots/phase2/phase2-img3.png" width="45%"
       />
  <img src="screenshots/phase2/phase2-img4.png" width="45%"
        />
</p>

<p align="center">
  <img src="screenshots/phase2/phase2-img5.png" width="45%"
       />
  <img src="screenshots/phase2/phase2-img6.png" width="45%"
        />
</p>