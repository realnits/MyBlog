---
author: Nithissh S
pubDatetime: 2025-01-27T15:22:00Z
modDatetime: 2025-01-27T07:12:47.400Z
title: Understanding IAM Basics
slug: understand-iam
featured: false
draft: false
tags:
  - CloudSec
description:
  Put in my notes as a blog for IAM in minimalist way
---


AWS Identity and Access Management (IAM) is fundamental to securing your cloud resources. This guide breaks down the essential concepts and components of IAM, helping you understand how to implement secure access controls in your AWS environment.

## Core IAM Primitives

IAM is built on three fundamental building blocks that work together to provide secure access management:

| Primitive | Description | Key Points |
|-----------|-------------|------------|
| User | An identity representing an individual or system | • Can be human or machine<br>• Has permanent long-term credentials<br>• Can belong to multiple groups |
| Role | A temporary identity with defined permissions | • Used for temporary access<br>• No permanent credentials<br>• Commonly used by applications and services |
| Policy | A document defining permissions | • Specifies allowed/denied actions<br>• Written in JSON<br>• Can be attached to users, roles, or resources |

## Understanding IAM Policies

### Policy Types

#### 1. Identity-based Policies
These policies are attached directly to IAM identities (users, groups, or roles) and specify what actions those identities can perform.

* **Inline Policies**
  - Embedded directly in a single user, group, or role
  - Cannot be reused across multiple identities
  - Useful for exceptional cases or one-off permissions
  - More difficult to manage at scale

* **Managed Policies**
  - Stand-alone policy objects that can be attached to multiple identities
  - Two subtypes:
    1. AWS Managed: Created and maintained by AWS
    2. Customer Managed: Created and maintained by you

#### 2. Resource-based Policies
Attached directly to resources (like S3 buckets or Lambda functions) to define who can access them and what actions they can perform.

### Policy Evaluation Fundamentals

1. **Default Deny Principle**
   - All access is denied by default
   - Access must be explicitly granted through policies
   - Provides a secure foundation for access control

2. **Policy Evaluation Logic**
   - Multiple policies are evaluated together
   - The final permission is determined by combining all applicable policies
   - Important rule: An explicit DENY always overrides any ALLOW

3. **Wildcard Usage**
   - Wildcards (`*`) can represent multiple characters
   - Example: `s3:*` represents all S3 actions
   - Use with caution as they can grant broader access than intended

## Policy Structure and Syntax

### Anatomy of an IAM Policy

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:GetObject",
                "s3:PutObject"
            ],
            "Resource": "arn:aws:s3:::bucket-name/*"
        }
    ]
}
```

### Key Elements Explained

| Element | Purpose | Example |
|---------|----------|---------|
| Version | Policy language version | "2012-10-17" (current version) |
| Statement | Container for permission rules | Array of policy statements |
| Effect | Specifies allow or deny | "Allow" or "Deny" |
| Action | API calls being controlled | "s3:GetObject" |
| Resource | Target of the permission | ARN of the resource |