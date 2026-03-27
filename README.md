# ashish-devops-blog

# 🚀 DevOps Blog Deployment using AWS + CI/CD

## 📌 Project Overview

This project demonstrates how to build and deploy a **static blog website** using:

* Hugo (Static Site Generator)
* Amazon S3 (Storage)
* Amazon CloudFront (CDN)
* GitHub Actions (CI/CD)

The goal is to implement a **production-ready DevOps pipeline** with automation and security.

---

## 🏗️ Architecture

User → CloudFront → S3 (Private)
GitHub → GitHub Actions → S3 → CloudFront

---

## ⚙️ Technologies Used

* Hugo
* AWS S3
* AWS CloudFront
* GitHub Actions
* IAM (for access control)

---

## 🚀 Features

* Static blog hosted on AWS
* Secure access using CloudFront (OAC)
* Automated deployment using CI/CD
* Cache invalidation after deployment
* No manual upload required

---

## 🧪 CI/CD Workflow

1. Code pushed to GitHub
2. GitHub Actions triggers pipeline
3. Hugo builds static site
4. Files uploaded to S3
5. CloudFront cache invalidated
6. Updated site is live

---

## ❌ Issues Faced & Fixes

### 🔴 1. 403 Access Denied (S3)

**Issue:**

* S3 bucket was private and not accessible

**Fix:**

* Added proper bucket policy
* Later secured using CloudFront OAC

---

### 🔴 2. 404 Not Found

**Issue:**

* `index.html` not found or incorrect structure

**Fix:**

* Uploaded correct `public/` folder content to S3
* Ensured `index.html` exists at root

---

### 🔴 3. CloudFront Access Denied

**Issue:**

* CloudFront could not access S3

**Fix:**

* Configured Origin Access Control (OAC)
* Updated S3 bucket policy to allow CloudFront

---

### 🔴 4. Git Push Rejected

**Issue:**

```bash
failed to push some refs
```

**Fix:**

```bash
git pull origin main --rebase
git push
```

---

### 🔴 5. GitHub Actions Failure (Exit Code 252)

**Issue:**

* AWS region not configured

**Fix:**

* Added:

```yaml
AWS_DEFAULT_REGION
```

---

### 🔴 6. CloudFront Invalidation Error

**Issue:**

* YAML formatting broke AWS CLI command

**Fix:**

* Used multiline syntax:

```yaml
run: |
  aws cloudfront create-invalidation ...
```

---

### 🔴 7. Theme Not Applied (Hugo)

**Issue:**

```bash
no layout file found
```

**Fix:**

* Enabled submodules in workflow:

```yaml
with:
  submodules: true
```

---

### 🔴 8. Hugo Version Mismatch

**Issue:**

* Theme required newer Hugo version

**Fix:**

* Installed latest Hugo in pipeline:

```bash
HUGO_VERSION=0.150.0
```

---

### 🔴 9. Google Analytics Partial Error

**Issue:**

```bash
partial "google_analytics.html" not found
```

**Fix:**

* Removed unnecessary analytics config

---

### 🔴 10. Changes Not Reflecting on Website

**Issue:**

* CloudFront cache serving old content

**Fix:**

* Added invalidation step:

```bash
/*
```

---

### 🔴 11. BaseURL Misconfiguration

**Issue:**

```toml
baseURL = "https://example.com"
```

**Fix:**

```toml
baseURL = "https://<cloudfront-url>"
```

---

## 🔐 Security Improvements

* S3 bucket made private
* Access only via CloudFront (OAC)
* No direct public access to S3

---

## 📈 Learning Outcomes

* Built end-to-end CI/CD pipeline
* Learned AWS S3 + CloudFront integration
* Understood caching & invalidation
* Debugged real-world DevOps issues
* Handled Git conflicts and CI/CD failures

---

## 🔗 Live Demo

👉 https://dl3vsxhqcuu7.cloudfront.net

---

## 🙌 Conclusion

This project demonstrates a real-world DevOps workflow with automation, security, and scalability using AWS and GitHub Actions.

---
