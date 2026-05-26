# 💻 EC2 Configuration Reference

> Full EC2 instance reference for the `aws-cloud-infra-lab` project.
> Both instances deployed inside `InfoTech-VPC` in `ca-central-1`.

---

## 🖥️ Instance Summary

| Name | OS | Type | Subnet | Access | Public IP |
|------|----|------|--------|--------|-----------|
| `InfoTech-Windows-Server` | Windows Server 2022 | t2.micro | Public | RDP 3389 | Yes |
| `InfoTech-Linux-Server` | Ubuntu 22.04 LTS | t2.micro | Private | SSH 22 | No |

---

## 🔑 Key Pair

| Item | Value |
|------|-------|
| **Name** | `InfoTech-KeyPair` |
| **Type** | RSA |
| **Format** | `.pem` |
| **Used For** | Windows password decryption + Linux SSH auth |
| **Storage** | `C:\Users\YourName\.ssh\InfoTech-KeyPair.pem` |

---

## 🪟 Windows Server Instance

| Setting | Value |
|---------|-------|
| **Instance Name** | `InfoTech-Windows-Server` |
| **AMI** | Windows Server 2022 Base |
| **Instance Type** | `t2.micro` |
| **VPC** | `InfoTech-VPC` |
| **Subnet** | `InfoTech-Public-Subnet` |
| **Public IP** | Auto-assigned (changes on restart) |
| **Security Group** | `InfoTech-Windows-SG` |
| **Storage** | 30 GB gp2 |
| **Username** | `Administrator` |
| **Password** | Decrypted via key pair |

**Connect via RDP:**
```
Remote Desktop Connection
Computer:  <Public IPv4>
Username:  Administrator
Password:  <from EC2 → Get Windows password>
```

---

## 🐧 Linux Server Instance

| Setting | Value |
|---------|-------|
| **Instance Name** | `InfoTech-Linux-Server` |
| **AMI** | Ubuntu Server 22.04 LTS |
| **Instance Type** | `t2.micro` |
| **VPC** | `InfoTech-VPC` |
| **Subnet** | `InfoTech-Private-Subnet` |
| **Public IP** | None |
| **Private IP** | `10.0.2.x` (assigned by AWS) |
| **Security Group** | `InfoTech-Linux-SG` |
| **Storage** | 8 GB gp2 |
| **Username** | `ubuntu` |

**Connect via SSH (from Windows Server):**
```bash
ssh -i "C:\InfoTech-KeyPair.pem" ubuntu@10.0.2.x
```

**Connect via Session Manager (browser):**
```
EC2 → Instances → InfoTech-Linux-Server → Connect → Session Manager
```

---

## ✅ Connectivity Verification

| Test | Command | Result |
|------|---------|--------|
| Windows → internet | `ping google.com` | ✅ |
| Linux → internet (NAT) | `ping google.com -c 4` | ✅ |
| Windows → Linux (internal) | `ping 10.0.2.x` | ✅ |
| Linux → Windows (internal) | `ping 10.0.1.x` | ✅ |

---

## ⚠️ Cost Management

| Item | Free Tier | Action |
|------|-----------|--------|
| EC2 compute | 750 hrs/month per instance | Stop when not in use |
| EBS storage | 30 GB/month | Within Free Tier |
| Public IP | Free while instance running | Released when stopped |
| Data transfer | 100 GB out/month | Monitor in billing |

> Stop both instances after each lab session.
> Public IP changes on restart unless an Elastic IP is assigned.

---

<div align="center">
<sub>💻 EC2 Configuration | aws-cloud-infra-lab | ca-central-1</sub>
</div>