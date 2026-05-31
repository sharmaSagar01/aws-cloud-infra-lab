# 📊 CloudWatch Configuration Reference

> Full monitoring and alerting reference for the `aws-cloud-infra-lab` project.
> Covers EC2 metrics, alarms, SNS notifications, dashboard, and VPC Flow Log queries.

---

## 📡 Monitored Resources

| Resource | Metrics | Frequency |
|----------|---------|-----------|
| `InfoTech-Windows-Server` | CPU, Network, Disk, Status | Every 5 min (basic) |
| `InfoTech-Linux-Server` | CPU, Network, Disk, Status | Every 5 min (basic) |
| `InfoTech-VPC` | Flow logs — all traffic | Continuous |

---

## 🔔 SNS Topic

| Item | Value |
|------|-------|
| **Topic Name** | `InfoTech-Alerts` |
| **Type** | Standard |
| **Subscription** | Email — confirmed |
| **Purpose** | Receives notifications from all CloudWatch alarms |

---

## ⚠️ CloudWatch Alarms

### InfoTech-HighCPU-Windows

| Field | Value |
|-------|-------|
| **Metric** | EC2 CPUUtilization |
| **Instance** | `InfoTech-Windows-Server` |
| **Statistic** | Average |
| **Period** | 5 minutes |
| **Condition** | Greater than 80% |
| **Action** | Notify InfoTech-Alerts (email) |
| **Test Result** | ✅ Alarm triggered — email received |

### InfoTech-StatusCheck-Windows

| Field | Value |
|-------|-------|
| **Metric** | StatusCheckFailed |
| **Instance** | `InfoTech-Windows-Server` |
| **Statistic** | Maximum |
| **Period** | 1 minute |
| **Condition** | Greater than or equal to 1 |
| **Action** | Notify InfoTech-Alerts (email) |

---

## 📊 Dashboard — InfoTech-Dashboard

| Widget | Type | Source |
|--------|------|--------|
| CPU Utilisation | Line graph | EC2 CPUUtilization |
| Network Traffic | Line graph | EC2 NetworkIn + NetworkOut |
| Alarm Status | Alarm status widget | Both alarms |
| VPC Flow Logs | Log table | `/aws/vpc/infotech-flow-logs` |

---

## 📋 Log Groups

| Log Group | Source | Status |
|-----------|--------|--------|
| `/aws/vpc/infotech-flow-logs` | VPC Flow Logs (Phase 2) | ✅ Active |

---

## 🔍 Useful Logs Insights Queries

```sql
-- All recent traffic
fields @timestamp, srcAddr, dstAddr, action, protocol
| sort @timestamp desc
| limit 50

-- Rejected traffic only
fields @timestamp, srcAddr, dstAddr, action
| filter action = "REJECT"
| sort @timestamp desc
| limit 20

-- Top source IPs by volume
stats sum(bytes) as totalBytes by srcAddr
| sort totalBytes desc
| limit 10
```

---

## 💡 Key CloudWatch Concepts Demonstrated

| Concept | Implementation |
|---------|---------------|
| EC2 metrics | Default metrics without any agent |
| SNS integration | Email alerts from CloudWatch alarms |
| Alarm thresholds | CPU at 80%, status check at 1 |
| Alarm testing | CPU stress test to trigger alert |
| Custom dashboard | All metrics in one consolidated view |
| Log Insights queries | VPC Flow Log analysis with SQL-style queries |

---

<div align="center">
<sub>📊 CloudWatch Configuration | aws-cloud-infra-lab | ca-central-1</sub>
</div>