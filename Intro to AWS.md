# Intro to AWS – Beginner-Friendly Notes

## What Is AWS?

**Amazon Web Services (AWS)** is Amazon’s massive cloud computing platform. Put simply, AWS lets you rent computers, storage, databases, and more over the internet, instead of owning that hardware yourself. From the biggest tech giants to small start-ups, hundreds of thousands of organisations use AWS every day for everything from streaming TV to running global websites.

## Why Is AWS a Big Deal?

- **Runs Many Apps You Use Daily** – Netflix, Dropbox, even McDonald’s make use of AWS under the hood.
- **Only Pay For What You Use** – There are no huge upfront costs; you’re billed for what you actually use, like electricity.
- **Flexible, Powerful, and Secure** – Spin up virtual machines, store heaps of data, automate setups, all with robust security tools.


## Quick History of AWS

- **2002:** Amazon originally built the AWS infrastructure for its own e-commerce, eventually realising how powerful it was.
- **2004:** AWS opened to the public, launching its first service—SQS (Simple Queue Service). At the time, this helped businesses handle messaging at scale.
- **2006:** Major public launch of now-famous services, including S3 (Simple Storage Service) and EC2 (Elastic Compute Cloud).
- **2007 onwards:** Rapid global expansion; AWS becomes the backbone of the modern cloud.
- **Today:** AWS is available across the globe and powers workloads for over a million businesses.


## AWS By the Numbers

- **\$35 billion annual revenue (2019):** That’s a serious chunk of the tech economy.
- **47% cloud market share (2019):** AWS is easily the market leader, ahead of Microsoft and Google.
- **Millions of users:** Everyone from micro-startups to the world’s largest enterprises rely on AWS.


## AWS Use Cases: What Can You Actually Do With It?

- **Build and Scale Applications:** From simple websites to apps handling millions of users.
- **Handle Massive Data:** Backup, storage, analysis—AWS handles it all for industries like IT, healthcare, and finance.
- **Media and Entertainment:** Netflix streams shows, Activision runs online games, and much more using AWS.
- **Cloud Storage:** Firms like Dropbox rely on AWS to deliver cloud storage for millions of people.
- **Global Operations:** Companies like McDonald’s use AWS to run and scale their worldwide digital infrastructure.

**Key Point:** AWS is trusted by almost every type of business, because it’s adaptable to almost any need.

## AWS Global Infrastructure

### Regions

- **What’s a Region?**
A distinct geographical area (like London or Tokyo) with a cluster of AWS data centres.
- **Why Does It Matter?**
    - Redundancy: More than one data centre means fewer outages.
    - Compliance: Some countries require data to stay within their borders.
    - Performance: A closer region means faster website/app loads for your users.
    - Price: Costs can vary between regions.

**Example:** If most of your users are in the UK, it’s usually best to choose a UK region for speed and privacy.

### Availability Zones (AZs)

- **Definition:**
Each region consists of 3–6 individual “availability zones” (think: separate, highly secure data centres).
- **Why?**
To ensure high availability and fault tolerance. If one AZ is affected by a failure or outage, the others keep your apps running.


### Points of Presence (Edge Locations)

- **What Are Edge Locations?**
Over 400 sites in 90+ cities, used mainly by AWS’s Content Delivery Network (CDN) called CloudFront.
- **Why Do They Matter?**
Closer “warehouses” for your data mean lower latency—so your content loads quicker for users, anywhere in the world.


## The AWS Console

- **What Is It?**
AWS’s web-based “command centre”. Here, you can create servers, set up storage, manage networking and security—all from one place.
- **Global vs Regional Services:**
    - Some services (like IAM, DNS/Route53, and CloudFront) are global—use them anywhere, not tied to a region.
    - Most AWS services (EC2, S3, Lambda, etc.) are regional—meaning you pick which region you want them to run in.


## Getting Started: Security and Billing Basics

- **Enable Multi-Factor Authentication (MFA):**
Add extra security to your AWS accounts.
- **Set Budgets and Alarms:**
Establish a budget and alerts in AWS’s billing dashboard to avoid surprise costs.
- **Don’t Use Your Root User:**
Always create an admin user via IAM (Identity \& Access Management) for daily tasks—using the root account is risky.


## Summary Table: Key AWS Concepts

| Concept | What It Is/Does | Why It Matters |
| :-- | :-- | :-- |
| Region | Geographical area with AWS data centres | Proximity, compliance, redundancy |
| Availability Zone | Individually-separated data centres in a region | High availability, resilience |
| Edge Location | Caches for rapid data delivery | Faster user experience everywhere |
| AWS Console | Web interface for managing AWS | Central place for setup and monitoring |
| Global Services | Not tied to a region (e.g., IAM, CloudFront) | Available from any region |
| Regional Services | Tied to a specific region (e.g., EC2, S3) | Lets you pick where your stuff lives |

## Final Cheat Sheet

- **AWS powers huge parts of the internet – but anyone can use it.**
- **Regions and AZs provide redundancy and resilience.**
- **Edge locations speed up content for users no matter where they are.**
- **The AWS console is your main control panel.**
- **Always secure your account: set up MFA, manage users properly, and set budget alarms.**

If you focus on these basics, you’ll go into future AWS chapters with a clear, practical understanding—without feeling lost in technical jargon.
