# 📖 AWS Cloud Infrastructure Lab — Operational Runbook

> Day-to-day operational reference for managing the AWS environment
> built in the `aws-cloud-infra-lab` project.
> Region: `ca-central-1` (Canada Central)

---

## 📑 Table of Contents

| # | Section |
|---|---------|
| 1 | [Environment Reference](#environment-reference) |
| 2 | [Session Startup Checklist](#session-startup-checklist) |
| 3 | [Session Shutdown Checklist](#session-shutdown-checklist) |
| 4 | [EC2 Management](#ec2-management) |
| 5 | [S3 Management](#s3-management) |
| 6 | [IAM Management](#iam-management) |
| 7 | [Monitoring & Alerts](#monitoring--alerts) |
| 8 | [Troubleshooting](#troubleshooting) |
| 9 | [Quick Reference](#quick-reference) |

---

## Environment Reference

| Resource | Name | Details |
|----------|------|---------|
| **Region** | ca-central-1 | Canada Central |
| **VPC** | `InfoTech-VPC` | `10.0.0.0/16` |
| **Public Subnet** | `InfoTech-Public-Subnet` | `10.0.1.0/24` — ca-central-1a |
| **Private Subnet** | `InfoTech-Private-Subnet` | `10.0.2.0/24` — ca-central-1b |
| **Windows EC2** | `InfoTech-Windows-Server` | t3.micro — public subnet |
| **Linux EC2** | `InfoTech-Linux-Server` | t3.micro — private subnet |
| **Main S3 Bucket** | `infotech-lab-bucket` | Private — versioned |
| **Static S3 Bucket** | `infotech-static-bucket` | Public — static website |
| **CloudWatch Dashboard** | `InfoTech-Dashboard` | CPU, network, alarms |
| **CloudTrail** | `InfoTech-AuditTrail` | All API calls logged |
| **SNS Topic** | `InfoTech-Alerts` | Email notifications |
| **IAM Admin** | `iamadmin` | Primary admin user |

---

## Session Startup Checklist

Before starting any lab work:

```
☐ Sign in as iamadmin — NOT root
☐ Confirm region is ca-central-1 (top right)
☐ EC2 → Start both instances
☐ Wait for 2/2 status checks to pass
☐ Note the new Public IP of Windows Server (changes on restart)
☐ Update Security Group RDP rule if your IP has changed
```

**Update Security Group after IP change:**
```
EC2 → Security Groups → InfoTech-Windows-SG
→ Inbound rules → Edit → RDP rule
→ Source: My IP → Save rules
```

---

## Session Shutdown Checklist

Before closing — always run through this to avoid unexpected charges:

```
☐ EC2 → Stop both instances
☐ VPC → NAT Gateways → Delete InfoTech-NAT-GW
☐ EC2 → Elastic IPs → Release any unattached IPs
☐ Billing → Free Tier usage → confirm within limits
```

**Recreate NAT Gateway next session:**
```
VPC → NAT Gateways → Create NAT gateway
Name: InfoTech-NAT-GW
Subnet: InfoTech-Public-Subnet
Allocate Elastic IP → Create

Then update private route table:
Route tables → InfoTech-Private-RT → Routes → Edit
0.0.0.0/0 → new NAT Gateway ID → Save
```

---

## EC2 Management

### Start / Stop Instances

```
EC2 → Instances → select instance
→ Instance state → Start / Stop
```

### Connect to Windows Server (RDP)

```
1. Get Public IP: EC2 → Instances → InfoTech-Windows-Server → Public IPv4
2. Get Password: Actions → Security → Get Windows password → upload .pem
3. Open Remote Desktop Connection
   Computer: <Public IPv4>
   Username: Administrator
   Password: <decrypted password>
```

### Connect to Linux Server (Session Manager)

```
EC2 → Instances → InfoTech-Linux-Server → Connect
→ Session Manager tab → Connect
```

### Connect to Linux Server (SSH via Windows EC2)

```powershell
# On Windows Server after RDP connection
ssh -i "C:\InfoTech-KeyPair.pem" ubuntu@<Linux-Private-IP>
```

### Check Instance Health

```
EC2 → Instances → Status check column
2/2 checks passed = healthy
1/2 or 0/2 = investigate in CloudWatch
```

---

## S3 Management

### Upload a File

```
S3 → infotech-lab-bucket → select folder → Upload → Add files
```

### View Object Versions

```
S3 → infotech-lab-bucket → Show versions toggle (top right)
```

### Restore a Deleted File

```
S3 → infotech-lab-bucket → Show versions → ON
→ Find the delete marker → select it → Delete
→ The file is restored
```

### Check Static Website

```
S3 → infotech-static-bucket → Properties
→ Static website hosting → Bucket website endpoint
→ Open in browser
```

---

## IAM Management

### Add a New User

```
IAM → Users → Create user
→ Assign to appropriate group (Admins / Developers / ReadOnly)
→ Enable MFA after creation
```

### Rotate Access Keys

```
IAM → Users → select user → Security credentials
→ Access keys → Create access key (new)
→ Update application/script with new key
→ Delete old key
```

### Review Permissions

```
IAM → Users → select user → Permissions tab
→ Confirm policies match the user's role
→ Use Access Advisor tab to see last service usage
```

---

## Monitoring & Alerts

### View CloudWatch Dashboard

```
CloudWatch → Dashboards → InfoTech-Dashboard
```

### Check Active Alarms

```
CloudWatch → Alarms → All alarms
→ Any In alarm state needs immediate attention
```

### Query VPC Flow Logs

```
CloudWatch → Logs → Logs Insights
→ Log group: /aws/vpc/infotech-flow-logs
```

```sql
-- Recent rejected traffic
fields @timestamp, srcAddr, dstAddr, action
| filter action = "REJECT"
| sort @timestamp desc
| limit 20
```

### View CloudTrail Events

```
CloudTrail → Event history
→ Filter by: Event name, User name, or Resource type
→ Useful for: who deleted a resource, who changed a security group
```

---

## Troubleshooting

| Symptom | First Check | Fix |
|---------|-------------|-----|
| Can't RDP to Windows EC2 | Security group — is your IP in the rule? | Update inbound RDP rule to My IP |
| Windows EC2 shows wrong password | IP changed after restart | Get Windows password again via EC2 console |
| Linux can't reach internet | NAT Gateway deleted or stopped | Recreate NAT GW, update private route table |
| S3 upload fails | Bucket policy blocking HTTP? | Use HTTPS — the HTTPS-only policy blocks HTTP |
| CloudWatch alarm stuck in insufficient data | Instance stopped | Start the instance |
| Free Tier usage warning | Check billing dashboard | Stop unused EC2, delete idle NAT Gateway |
| Security group change not working | Wrong security group edited | Confirm SG is attached to the correct instance |

---

## Quick Reference

```
# AWS Console URLs
Sign in (IAM):    https://YOUR-ACCOUNT-ID.signin.aws.amazon.com/console
EC2 Console:      ca-central-1.console.aws.amazon.com/ec2
S3 Console:       s3.console.aws.amazon.com
CloudWatch:       ca-central-1.console.aws.amazon.com/cloudwatch
IAM:              console.aws.amazon.com/iam
CloudTrail:       ca-central-1.console.aws.amazon.com/cloudtrailv2
VPC:              ca-central-1.console.aws.amazon.com/vpc
```

```
# Free Tier limits to watch
EC2 t3.micro:     750 hrs/month total — stop when not in use
S3 storage:       5 GB — monitor bucket sizes
CloudWatch:       10 metrics, 5 GB logs — within lab usage
Data transfer:    100 GB out/month — well within lab usage
NAT Gateway:      ~$0.045/hr — DELETE between sessions
```

---

<div align="center">
<sub>📖 Operational Runbook | aws-cloud-infra-lab | ca-central-1</sub>
</div>