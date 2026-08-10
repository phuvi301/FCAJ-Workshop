---
title: "Introduction & Overview"
date: 2026-07-30
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

### Introduction to CodExecute

**CodExecute** is a modern Online Judge platform and developer social network designed to compile, execute, and evaluate user-submitted code (C++, Java, Python, JavaScript) in real time.

Built on a **Pure Serverless Cloud-Native AWS** architecture, CodExecute addresses 3 primary operational challenges of traditional online judge systems:
1. **RCE Prevention & Sandbox Security:** Fully isolating unverified user code within an **AWS Lambda Worker Sandbox** runtime with restricted permissions and disabled outbound network access.
2. **Handling Submission Spikes:** Utilizing **Amazon SQS** as an asynchronous buffer queue to absorb traffic spikes without system degradation or downtime.
3. **Cost Optimization (Pay-As-You-Go):** Auto-scaling infrastructure from 0 (Scale-to-Zero) during idle hours, reducing server costs by up to 75%.

---

### System Architecture Overview

CodExecute operates through the seamless integration of 8 core AWS services:

* **Amazon CloudFront & Amazon S3:** Global edge distribution for the React Frontend application and secure storage for testcase datasets (Input/Output text files).
* **Amazon API Gateway & AWS Lambda (API Handler):** Serves RESTful API endpoints and executes backend business logic.
* **Amazon SQS (Submissions Queue):** Buffers incoming code submissions for asynchronous processing by evaluation workers.
* **AWS Lambda (Worker Sandbox Runner):** Polls jobs from SQS, fetches testcases from S3, and executes code in an isolated sandbox environment.
* **Amazon DynamoDB:** High-performance NoSQL database storing user profiles, problemsets, submissions, and social interactions.
* **Amazon CloudWatch & AWS IAM:** Real-time logging, performance alarm metrics, and Least Privilege Access control.

<div align="center">

<img src="/images/2-Proposal/architect-codexecute.drawio.png" alt="CodExecute Architecture Diagram" style="width: 70%; max-width: 900px; border-radius: 6px;">

<p style="font-size: 1.15rem; font-weight: 600; margin-top: 8px;">
<i>Figure 1: CodExecute AWS Serverless System Architecture Diagram</i>
</p>

<img src="/images/5-Workshop/5.1-Workshop-overview/project_overview.png" alt="CodExecute Webpage" style="width: 80%; max-width: 1100px; border-radius: 6px;">
<p style="font-size: 1.15rem; font-weight: 600; margin-top: 8px;">
<i>Figure 2: CodExecute Webpage</i></br>
<i>Link webpage: </i><a target="blank" href="https://d1hsp5bm4hkjmb.cloudfront.net/">d1hsp5bm4hkjmb.cloudfront.net</a></br>
<i>Link demo: </i><a target="blank" href="https://drive.google.com/file/d/15AeqXtTXdVslTlJy3HmrP7IP6lOOiFaS/view?usp=sharing">Click here</a>
</p>

</div>