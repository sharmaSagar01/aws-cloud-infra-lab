# 🔐 IAM Configuration Reference

> Full IAM setup reference for the `aws-cloud-infra-lab` project.
> Covers root account security, admin user, groups, users, and custom policies.

---

## 🌐 Account Details

| Item | Value |
|------|-------|
| **AWS Region** | `ca-central-1` (Canada Central) |
| **Account Type** | Free Tier |
| **Root MFA** | ✅ Enabled |
| **Root Access Keys** | ✅ Deleted |
| **IAM Sign-in URL** | `https://YOUR-ACCOUNT-ID.signin.aws.amazon.com/console` |

---

## 👤 IAM Users

| Username | Group | Access Type | MFA | Purpose |
|----------|-------|-------------|-----|---------|
| `iamadmin` | Admins | Console | ✅ Enabled | Primary admin — all lab work |
| `dev-user` | Developers | Console | ⏳ Optional | Simulates developer account |
| `readonly-user` | ReadOnly | Console | ⏳ Optional | Simulates auditor account |

---

## 👥 IAM Groups

| Group | Policy | Purpose |
|-------|--------|---------|
| `Admins` | AdministratorAccess (AWS Managed) | Full admin access |
| `Developers` | PowerUserAccess (AWS Managed) | All services except IAM |
| `ReadOnly` | ReadOnlyAccess (AWS Managed) | View-only access |

---

## 📋 Custom IAM Policy

**Policy Name:** `S3ReadOnly-InfoTechBucket`

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "S3ReadOnlySpecificBucket",
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:ListBucket"
      ],
      "Resource": [
        "arn:aws:s3:::infotech-lab-bucket",
        "arn:aws:s3:::infotech-lab-bucket/*"
      ]
    }
  ]
}
```

| Field | Value |
|-------|-------|
| **Effect** | Allow |
| **Actions** | GetObject, ListBucket |
| **Scope** | Single bucket — `infotech-lab-bucket` |
| **Assigned To** | `readonly-user` |

---

## 🔒 Password Policy

| Setting | Value |
|---------|-------|
| Minimum length | 12 characters |
| Require uppercase | Yes |
| Require numbers | Yes |
| Require symbols | Yes |
| Password expiry | 90 days |
| Prevent reuse | Last 3 passwords |

---

## ✅ IAM Security Dashboard Status

| Check | Status |
|-------|--------|
| Root MFA enabled | ✅ |
| Root access keys deleted | ✅ |
| IAM admin user created | ✅ |
| Admin user MFA enabled | ✅ |
| Password policy configured | ✅ |

---

## 💡 Key IAM Concepts Demonstrated

| Concept | Implementation |
|---------|---------------|
| Least privilege | Custom S3 policy scoped to one bucket only |
| Group-based permissions | Permissions assigned to groups not individuals |
| MFA enforcement | Enabled on root and iamadmin |
| Root account security | MFA enabled, access keys deleted, root not used |
| Managed vs custom policies | Both used — AdministratorAccess managed, S3 custom |

---

<div align="center">
<sub>🔐 IAM Configuration | aws-cloud-infra-lab | ca-central-1</sub>
</div>