# 🪣 S3 Configuration Reference

> Full S3 storage reference for the `aws-cloud-infra-lab` project.
> Two buckets — one private for lab storage, one public for static website.

---

## 🗂️ Buckets Summary

| Bucket | Access | Versioning | Encryption | Purpose |
|--------|--------|-----------|------------|---------|
| `infotech-lab-bucket` | Private | ✅ Enabled | SSE-S3 | Lab storage — logs, backups, configs |
| `infotech-static-bucket` | Public (read) | ❌ Disabled | SSE-S3 | Static website hosting |

---

## 🔒 Main Bucket — `infotech-lab-bucket`

| Setting | Value |
|---------|-------|
| **Region** | `ca-central-1` |
| **Block Public Access** | All blocked ✅ |
| **Versioning** | Enabled |
| **Encryption** | SSE-S3 (Amazon managed keys) |
| **Object Ownership** | ACLs disabled |

### Folder Structure

| Folder | Purpose |
|--------|---------|
| `logs/` | VPC flow logs and EC2 logs |
| `backups/` | Simulated server backup files |
| `configs/` | Configuration file storage |

### Bucket Policy — HTTPS Only

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "DenyNonHTTPS",
      "Effect": "Deny",
      "Principal": "*",
      "Action": "s3:*",
      "Resource": [
        "arn:aws:s3:::infotech-lab-bucket",
        "arn:aws:s3:::infotech-lab-bucket/*"
      ],
      "Condition": {
        "Bool": {
          "aws:SecureTransport": "false"
        }
      }
    }
  ]
}
```

---

## 🌐 Static Website Bucket — `infotech-static-bucket`

| Setting | Value |
|---------|-------|
| **Region** | `ca-central-1` |
| **Block Public Access** | Disabled — public read allowed |
| **Static Website Hosting** | Enabled |
| **Index Document** | `index.html` |
| **Website Endpoint** | `http://infotech-static-bucket.s3-website.ca-central-1.amazonaws.com` |

### Bucket Policy — Public Read

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadAccess",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::infotech-static-bucket/*"
    }
  ]
}
```

---

## 🔄 Lifecycle Rules

| Rule | Scope | Action | After |
|------|-------|--------|-------|
| `archive-old-logs` | `logs/` prefix | Transition to Glacier | 30 days |
| `archive-old-logs` | `logs/` prefix | Delete | 365 days |
| `expire-old-backups` | `backups/` prefix | Delete current versions | 90 days |

---

## 🧪 Versioning Test

| Test | Result |
|------|--------|
| Upload v1 of test.txt | ✅ |
| Upload v2 of same file | ✅ Both versions visible |
| Delete latest version | ✅ Delete marker created |
| Restore by deleting marker | ✅ File recovered |

---

## 💡 Key S3 Concepts Demonstrated

| Concept | Implementation |
|---------|---------------|
| Private vs public buckets | Separate buckets with different access policies |
| Bucket policies | HTTPS-only enforcement + public read for static site |
| Versioning | Every object version retained — recovery tested |
| Lifecycle rules | Automatic archiving to Glacier and expiration |
| Static website hosting | Public HTML page served from S3 endpoint |
| Encryption at rest | SSE-S3 on both buckets |

---

<div align="center">
<sub>🪣 S3 Configuration | aws-cloud-infra-lab | ca-central-1</sub>
</div>