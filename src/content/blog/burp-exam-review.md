---
author: Nithissh S
pubDatetime: 2025-01-22T15:22:00Z
modDatetime: 2025-01-22T07:12:47.400Z
title: BurpSuite Certified Practitioner Exam Review 
slug: bscp-exam-review
featured: true
draft: false
tags:
  - AppSec
description:
  Some interesting learning on how we can find a way to get account ID through public s3 bucket 
---

# My Journey to Becoming a Burp Suite Certified Practitioner

I recently passed the Burp Suite Certified Practitioner (BSCP) exam on my first attempt, and I'm excited to share my journey, preparation strategy, and insights that might help others pursuing this certification. The exam tests your web security knowledge and practical skills in a time-constrained environment, making thorough preparation essential.

## Background and Initial Struggles

My preparation journey spanned about 4 months, though I'll admit the first two months weren't as productive as they could have been. Before PortSwigger announced the certification, I had already completed various labs covering XSS, SQL injection, Access control, and Business logic vulnerabilities. However, I often took shortcuts by jumping straight to solutions without deeply understanding the underlying concepts.

While looking at solutions isn't inherently wrong, I was missing crucial aspects:
- Understanding how the vulnerabilities work at a fundamental level
- Learning the methodology behind exploitation
- Developing a systematic approach to problem-solving

## The Turning Point

Everything changed when my organization offered me the opportunity to take the exam. I decided to reboot my approach to web security learning, starting from scratch. Here's how I restructured my preparation:

1. Created a comprehensive todo list of all labs
2. Started with familiar concepts to build confidence
3. Gradually progressed to more challenging topics
4. Focused on understanding rather than just completing labs

## Effective Preparation Strategy

### Phase 1: Tackling the Hard Stuff First
I identified and prioritized challenging topics I wasn't comfortable with:
- HTTP Request Smuggling
- Insecure Deserialization
- Web Cache Poisoning

For each of these topics, I:
- Completed all related labs
- Took on mystery lab challenges to improve reconnaissance skills
- Documented my methodology and key learnings

### Phase 2: Reinforcing Fundamentals
After mastering the challenging topics, I revisited "easier" vulnerabilities:
- Access Control
- SSRF
- File Upload Vulnerabilities

I completed all apprentice and practitioner-level labs in these categories, followed by mystery labs to sharpen my identification skills.

### Phase 3: Exam Preparation
- Took 4-5 practice exams to get comfortable with time constraints
- Focused on quick vulnerability identification
- Practiced efficient exploitation techniques

### Useful Resources 

- [Burp Suite Certified Practitioner Exam Study from Botesjuan](https://github.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study) - This is will helpful referring as guide / Handbook during exam 
- [Ultimate BSCP guide from dingyshark](https://github.com/DingyShark/BurpSuiteCertifiedPractitioner) - Same like the previous one, But some extras added which were helpful actually 

## Technical Tips and Considerations

1. **For MacBook Users**
   - Use JDK v11 for Java deserialization scanner
   - Ensures compatibility and optimal performance

2. **XSS Preparation**
   - Maintain a collection of cookie-stealing payloads
   - Document successful exploitation techniques

## Key Takeaways

1. **Avoid Shortcuts**
   - Understanding concepts is more important than rushing through labs
   - Take time to analyze why exploits work

2. **Progressive Learning**
   - Start with challenging topics
   - Use mystery labs to develop real-world skills
   - Reinforce fundamentals through practice

3. **Time Management**
   - Practice working under time constraints
   - Develop efficient methodology through practice exams

Remember, the journey to BSCP certification is not just about passing an exam—it's about building a solid foundation in web security. Take your time to understand concepts thoroughly, and don't hesitate to revisit challenging topics until they become second nature.
