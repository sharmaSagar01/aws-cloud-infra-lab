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
│   ├── iam-config.md          # IAM users, groups, roles, policies     ⏳
│   ├── vpc-config.md          # VPC, subnets, route tables, SGs        ⏳
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

| # | Phase | Status |
|---|-------|--------|
| 1 | AWS Free Tier setup + IAM users, groups, and MFA | ⏳ Pending |
| 2 | Custom VPC — subnets, route tables, security groups, internet gateway | ⏳ Pending |
| 3 | EC2 — launch Windows and Linux instances, connect via RDP and SSH | ⏳ Pending |
| 4 | S3 — buckets, policies, versioning, and lifecycle rules | ⏳ Pending |
| 5 | CloudWatch — monitoring, alarms, dashboards, and log groups | ⏳ Pending |
| 6 | IAM hardening + AWS security best practices | ⏳ Pending |
| 7 | Runbook + final documentation + GitHub push | ⏳ Pending |

---

## 🎯 What You Will Have at the End

| Capability | Details |
|------------|---------|
| **Cloud Networking** | Custom VPC with public and private subnets |
| **Compute** | Windows Server and Ubuntu EC2 instances |
| **Identity** | IAM users, groups, roles, and least-privilege policies |
| **Storage** | S3 buckets with policies, versioning, and lifecycle management |
| **Monitoring** | CloudWatch dashboards, alarms, and log groups |
| **Security** | MFA on root, least-privilege IAM, security groups, hardened config |

---

## ⚙️ Prerequisites

**AWS Free Tier includes (sufficient for this project):**

| Service | Free Tier Limit |
|---------|----------------|
| EC2 | 750 hours/month — `t2.micro` |
| S3 | 5 GB storage |
| CloudWatch | 10 custom metrics, 5 GB log data |
| IAM | Always free |
| VPC | Always free |
| Data Transfer | 100 GB out/month |

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

<div align="center">
<sub>☁️ Built for learning • ⭐ Star if you find this useful • More phases coming soon</sub>
</div>