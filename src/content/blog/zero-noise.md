---
author: Nithissh S
pubDatetime: 2025-06-03T20:00:00Z
modDatetime: 2025-06-03T20:00:00Z
title: The Zero Noise Approach to Cloud Detection
slug: zero-noise-cloud-detection
featured: false
draft: false
tags:
  - CloudSec
  - Detection Engineering
  - SOC
  - Wiz
description:
  Learn how to reduce alert fatigue and prioritize high-fidelity detections using Wiz's Zero Noise Approach. Tailor alerts, implement feedback loops, and ensure outcome-based triaging for real-world SOC efficiency.
---

### Key Challenge

Most organizations rely heavily on public cloud providers like AWS, Azure, and GCP. This shared architecture means many companies experience similar threats—and that leads to an avalanche of alerts.  
High alert volume → **alert fatigue** → missed or delayed real threat responses.

---

### The Zero Noise Approach

A structured detection engineering model to cut down noise and increase detection fidelity.

---

### 1. Alerts with an Attacker’s Perspective

**Problem**: Generic alerts cause too much noise and little signal.

**Solution**: Build detections that mimic attacker behaviors:

- Align with **environmental baselines** and **critical assets**.
- Model alerts based on known attacker **TTPs** (MITRE-style).
- Use continuous red teaming to detect **visibility gaps**.
  
Tailor alerts → increase fidelity → reduce noise.

---

### 2. Detection Feedback Loops

**Problem**: SOC teams drown in unfiltered detections.

**Solution**: Regularly review each detection rule:

- How often it triggers?
- What’s the false positive rate?
- How long does triage take?

Then act:
- **Remove** if noisy.
- **Improve** logic (thresholds, exclusions).
- **Refactor** internal processes if needed.

---

### 3. No Alert Left Behind

**Problem**: False positives are often left unresolved.

**Solution**: Mandate **triage for every alert**.

- **True Positive** → Initiate response playbook.
- **False Positive** → Refine detection or suppress noise.

**Triage Outcomes**:
- Remove detection (irrelevant).
- Improve logic (tighten scope).
- Update internal practices (adjust dev/ops to avoid unnecessary alerts).

---

### Real-World Case Study – Financial Services Firm

**Issue**:
- Attackers faking PoS transactions.
- Legacy infra + wide-scope rules = massive alert volume and missed true positives.

**Applied Fixes**:
- Tailored alert for suspicious transaction server activity → Early threat detection.
- Removed noisy DMZ server detections → SOC time saved.
- Tuned load balancer alerts → Reduced false positives.
- Blocked PsExec (used by IT and attackers) → Clean IOC identified.

---

### Outcome

- **Noise reduction** → Clearer signal.
- **Higher SOC efficiency** → Reduced burnout.
- **Improved response time** → Prevented financial damage.

---

Reference:  
[Wiz Blog - The Zero Noise Approach to Cloud Detection](https://www.wiz.io/blog/the-zero-noise-approach-to-cloud-detection?utm_source=cloudseclist.com&utm_medium=referral&utm_campaign=CloudSecList-issue-279)