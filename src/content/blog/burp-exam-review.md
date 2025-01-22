---
author: Nithissh S
pubDatetime: 2025-01-22T15:22:00Z
modDatetime: 2025-01-22T09:12:47.400Z
title: BurpSuite Certified Practitioner Exam Review 
slug: bscp-exam-review
featured: true
draft: false
tags:
  - AppSec
description:
  I recently cleared the Burp Suite Certified Practitioner exam, and it was quite the journey! In this post, I’ll share my experiences, tips, and key takeaways to help anyone planning to take the exam or explore the PortSwigger Academy challenges. Let’s dive in!
---

### Introduction

I recently cleared the Burp Suite Certified Practitioner exam, and it was quite the journey! In this post, I’ll share my experiences, tips, and key takeaways to help anyone planning to take the exam or explore the PortSwigger Academy challenges. Let’s dive in!

### A Little Backstory

It took me nearly four months to prepare for this certification, but let me start by admitting how I wasted the first two months. Even before PortSwigger announced their certification, I had already completed several labs, including XSS, SQL injection, access control, business logic flaws, and many others. However, I often skipped the harder challenges or resorted to shortcuts like looking up solutions and solving them directly.

While looking at solutions can be helpful, it’s not effective if you don’t truly understand the context, like how the vulnerability works and how to exploit it. This lack of depth in my approach eventually became apparent.

Thankfully, my organization provided me with the opportunity to take this exam. I decided to reboot my web security knowledge by starting from scratch. I began pre-planning by creating a to-do list of all the labs and committed to solving them day by day. Initially, I gravitated toward the challenges I was comfortable with, avoiding the harder ones. However, I quickly realized that sticking to easy labs wasn’t helping me grow. Challenges like blind SQL injection, request smuggling, and deserialization felt tough, but they were the ones that taught me the most.

### How Did I Prepare?

Here’s how I structured my preparation over the last few months:

1. **Focus on the Unknown:**
   - I listed vulnerabilities I wasn’t confident about, such as request smuggling, deserialization, and web cache poisoning.
   - Solving these challenges helped me build foundational knowledge and confidence.

2. **Mystery Labs:**
   - After completing the basic challenges, I tackled the mystery labs for these vulnerabilities. These labs improved my recon skills, helping me identify and exploit vulnerabilities more effectively.

3. **Mastering the Basics:**
   - I revisited easier challenges like access control, SSRF, and file uploads. Completing all the apprentice and practitioner labs gave me a solid grip on the fundamentals.
   - I then revisited the mystery labs for these topics to deepen my understanding.

4. **Practice Exams:**
   - Once I completed the required labs, I took the practice exams 4-5 times. This helped me get comfortable identifying vulnerabilities within a limited timeframe and prepared me well for the actual exam.

### Useful Resources

- [Burp Suite Certified Practitioner Exam Study by Botesjuan](https://github.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study): A great guide/handbook to refer to during the exam.
- [Ultimate BSCP Guide by DingyShark](https://github.com/DingyShark/BurpSuiteCertifiedPractitioner): Similar to the previous guide but with additional helpful insights.

### Key Tips to Remember

- **MacBook Users:** If you’re taking the exam on a Mac, use JDK v11 for the Java deserialization scanner.
- **Tracking Payloads:** While solving labs like XSS, keep track of your payloads for cookie stealing. Many useful payloads are available in the repositories mentioned above.

By staying consistent and focusing on both the basics and harder challenges, I was able to pass the exam and deepen my understanding of web security. If you’re preparing for the Burp Suite Certified Practitioner exam, I hope these tips and resources help you on your journey. Good luck!