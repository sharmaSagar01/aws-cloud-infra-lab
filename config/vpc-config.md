# 🌐 VPC Configuration Reference

> Full networking reference for the `aws-cloud-infra-lab` project.
> All resources deployed in `ca-central-1` (Canada Central).

---

## 🏗️ VPC

| Item | Value |
|------|-------|
| **VPC Name** | `InfoTech-VPC` |
| **CIDR Block** | `10.0.0.0/16` |
| **Region** | `ca-central-1` |
| **DNS Hostnames** | Enabled |
| **DNS Resolution** | Enabled |

---

## 🗂️ Subnets

| Name | CIDR | AZ | Type | Auto-assign Public IP |
|------|------|----|------|-----------------------|
| `InfoTech-Public-Subnet` | `10.0.1.0/24` | `ca-central-1a` | Public | ✅ Enabled |
| `InfoTech-Private-Subnet` | `10.0.2.0/24` | `ca-central-1b` | Private | ❌ Disabled |

---

## 🌍 Internet Gateway

| Item | Value |
|------|-------|
| **Name** | `InfoTech-IGW` |
| **State** | Attached |
| **Attached To** | `InfoTech-VPC` |

---

## 🔀 Route Tables

**Public Route Table — `InfoTech-Public-RT`**

| Destination | Target | Purpose |
|-------------|--------|---------|
| `10.0.0.0/16` | Local | Internal VPC traffic |
| `0.0.0.0/0` | `InfoTech-IGW` | Internet access |

Associated with: `InfoTech-Public-Subnet`

---

**Private Route Table — `InfoTech-Private-RT`**

| Destination | Target | Purpose |
|-------------|--------|---------|
| `10.0.0.0/16` | Local | Internal VPC traffic |
| `0.0.0.0/0` | `InfoTech-NAT-GW` | Outbound internet via NAT |

Associated with: `InfoTech-Private-Subnet`

---

## 🔁 NAT Gateway

| Item | Value |
|------|-------|
| **Name** | `InfoTech-NAT-GW` |
| **Subnet** | `InfoTech-Public-Subnet` |
| **Connectivity** | Public |
| **Elastic IP** | Allocated |
| **State** | Available |

> ⚠️ Delete when not in use — ~$0.045/hour charge applies.

---

## 🔒 Security Groups

**`InfoTech-Windows-SG`**

| Direction | Type | Protocol | Port | Source |
|-----------|------|----------|------|--------|
| Inbound | RDP | TCP | 3389 | My IP |
| Inbound | ICMP | All | All | `10.0.0.0/16` |
| Outbound | All | All | All | `0.0.0.0/0` |

Used by: Windows Server EC2 (Phase 3)

---

**`InfoTech-Linux-SG`**

| Direction | Type | Protocol | Port | Source |
|-----------|------|----------|------|--------|
| Inbound | SSH | TCP | 22 | My IP |
| Inbound | ICMP | All | All | `10.0.0.0/16` |
| Outbound | All | All | All | `0.0.0.0/0` |

Used by: Ubuntu Linux EC2 (Phase 3)

---

## 📊 VPC Flow Logs

| Item | Value |
|------|-------|
| **Filter** | All traffic |
| **Destination** | CloudWatch Logs |
| **Log Group** | `/aws/vpc/infotech-flow-logs` |
| **Status** | Active |

---

## 💡 Key Networking Concepts Demonstrated

| Concept | Implementation |
|---------|---------------|
| Public vs private subnets | Public has IGW route, private uses NAT |
| Internet Gateway | Enables inbound and outbound internet for public subnet |
| NAT Gateway | Outbound-only internet access for private subnet |
| Route tables | Separate tables per subnet controlling traffic flow |
| Security groups | Stateful firewall at instance level — port and source specific |
| VPC Flow Logs | Full network traffic capture for auditing and troubleshooting |
| Availability zones | Subnets in separate AZs for fault tolerance |

---

<div align="center">
<sub>🌐 VPC Configuration | aws-cloud-infra-lab | ca-central-1</sub>
</div>