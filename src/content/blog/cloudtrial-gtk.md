---
author: Nithissh S
pubDatetime: 2024-01-04T11:22:00Z
modDatetime: 2024-01-04T11:22:00Z
title: Getting to know about Cloudtrial
slug: cloudtrial-gtk
featured: false
draft: false
tags:
  - AWS
description:
  Getting to know about cloudtrial in a such a way to understad easily
--- 

## Overview

- Tracks management plane API activity (admin actions) in AWS.  
- 90-day retention by default; save logs to S3 for long-term storage.  
- Multi-region trails enable centralized logging across all AWS regions.  

### Types of Logs:
- **Management Events:** Free, logs admin API actions (default).  
- **Data Events:** Tracks resource access (e.g., S3 buckets), incurs extra cost.  
- **Insights Events:** Paid feature, detects unusual activity patterns.  

### S3 Costs:
- Saving logs incurs charges; manage with lifecycle policies (e.g., auto-delete after 3 months).  
- Enable an all-regions trail for centralized logging.  
- Use default S3 encryption for simplicity and security.  
- Enable log file validation for forensic accuracy.  

### Gaps in Logs:
- Some API activity may not be captured due to service inconsistencies.  
- Undocumented APIs or excluded activities (e.g., read actions in Microsoft services).  
- **Regional Isolation:** AWS regions are separate; trails must be configured for each region.  

- Provides a single source of truth for administrative activity.  
- Improves visibility and strengthens cloud security monitoring.  