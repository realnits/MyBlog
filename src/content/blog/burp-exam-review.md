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

### Introduction 

I recently cleared the Burp Suite Certified Practitioner exam, and it was quite the journey! In this post, I’ll share my experiences, tips, and key takeaways to help those of you planning to take the exam or explore the PortSwigger Academy challenges. Let’s dive in!

### Just a dirt background... 

It's been quite a journey for almost 4 months completely and let me explain you how i wasted my first 2 months while preparing for this certification actually.. Before even portswigger announced there certification back in time, I've completed the several labs like XSS, SQL injection, Access control, Business logics and most of the other labs..  But often ignored the hard things actually or took the shortcut paths like looking into the solution and solving directly.. 

Looking into the solution is fine but without understanding the context of exploitation like how the bug works? and how to exploit? and these things i don't understand 

But recently my organization provided with the opportunity to take this exam actually and I thought why can't we do like reboot our web security knowledge like starting from scratch... Like entered into the pre-planning phase like making todolist of all the labs and day to day, I started solving the ones I was comfortable with rather than learning something hard.. Why I say hard things? Hard things are the ones you will learn something new and rather than getting comfortable with easy ones and eventually you won't learn because in my perspective when after completing half of the easy labs like XSS, Access control, File uploads.. I lost interest in solving hard challenges like Blind SQLi, Request smuggling and deserialization just because it's tough 

Let's have a look into how did I prepare in last few months and things that helped me out 

### Well, How did I prepare?

- First things first, do stuffs you don't about and for me I listed vulnerabilities such as request smuggling, deserialization, Web cache poisoning 
- Once after solving those challenges, eventually I took the mystery lab challenges on those labs and you can ask why mystery labs.. it will help out in improving recon skills to identify and exploit those vulnerabilities 
- Next up the easy ones like Access control, SSRF, File upload and some others like these are easy challenges from my perspective and completed all the apprentice and practitioner labs. then took the mystery labs again for the easy challenge part 
- Once after completing all the required labs for the exam, I took the practice exams around 4 - 5 times until I'm comfortable in identifying the vulnerabilities in limited amount of time to get prepared for the exam 

### Useful Resources 

- [Burp Suite Certified Practitioner Exam Study from Botesjuan](https://github.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study) - This is will helpful referring as guide / Handbook during exam 
- [Ultimate BSCP guide from dingyshark](https://github.com/DingyShark/BurpSuiteCertifiedPractitioner) - Same like the previous one, But some extras added which were helpful actually 

### Things to remember

- If you are using macbook for the exam, try to utilise jdkv11 for utilising java deserialization scanner 
- While solving labs such as XSS, Keep track of payloads for cookie stealing and most of thing will be available in above mentioned repositories