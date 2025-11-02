# Week 1: AWS Global Infrastructure Fundamentals

## 52-Week AWS Solution Architect Roadmap

---

## Overview

This week covers the foundational concepts of AWS Global Infrastructure, focusing on how AWS distributes and organizes its services across the globe for high availability, low latency, and disaster recovery.

---

## 1. AWS Infrastructure Components

### Geographic Distribution
AWS infrastructure is **globally distributed** and designed for high availability. It consists of:
- **Regions**: Isolated geographical locations (e.g., India, Mumbai, Hyderabad)
- **Availability Zones (AZs)**: Multiple data centers within each region
- **Edge Locations**: Content delivery network endpoints

---

## 2. AWS Regions

### What are AWS Regions?

A **Region** is a physical location around the world where AWS clusters data centers.

### Key Characteristics:
- Geographically isolated locations
- Each region contains **multiple Availability Zones**
- Fully independent from other regions
- Data **never leaves the region** without explicit permissions

### Why do we have AWS Regions?

#### Compliance & Data Residency
- Ensures data never leaves the region without explicit permissions
- Helps meet legal and regulatory requirements (e.g., GDPR)

#### Proximity to Customers
- Choosing a closer region reduces **latency** and improves performance
- Serves residents, thus lowering the overall distance for every request to reduce roll-out

#### Service Availability
- Not all AWS services are available in every region
- Some services or features may launch in specific regions before others
- Pricing may also vary by region

### Available Regions in India:
- **Mumbai**
- **Hyderabad**

---

## 3. Availability Zones (AZs)

### What are Availability Zones?

**Availability Zones** are physically separated data centers within a region, each with their own independent:
- Power supply
- Cooling systems
- Networking infrastructure
- Security systems

Connected by **high-speed, low-latency network** links.

### Benefits:

#### Fault Isolation
Fault/Failure in one zone is **not supposed to affect others**

#### High Availability Architecture
- **EC2 auto scaling**
- **Multi-AZ RDS**
- **Disaster recovery**

#### Edge-Based Services
- **CloudFront**: Content Delivery Network (CDN)
- **Route 53**: DNS service
- Delivers low-latency content to users globally

### Disaster Recovery
Reduces the latency by bringing the AWS services closer to users.

---

## 4. Edge Locations

### What are Edge Locations?

**Edge locations** serve as content delivery endpoints that return a **fast response** to users.

### How They Work:
When a user requests content at an edge location:
1. If **cached**, serves the content immediately
2. If **not cached**, fetches from origin, stores it, then serves
3. Subsequently serves from cache for faster delivery

### Key Characteristics:
- Physically much closer to users than the origin server
- Lower latency for end users
- Content is served directly from the cache

### Services Using Edge Locations:

#### CloudFront (CDN)
- Caches static content (images, videos, etc.) at edge locations
- Reduces latency by 80% for distributed database solutions

#### Route 53 (DNS)
- Serves DNS responses from edge locations
- Allows queries that originate nearby to resolve faster
- Prevents traffic in edge locations to stop unwanted traffic

#### Use Cases:
- Streaming, gaming, and global websites

### Available Edge Locations in India:
- **Bengaluru**
- **Chennai**
- **Mumbai**
- **Pune**
- **Kolkata**
- **Hyderabad**

---

## 5. Local Zones (Optional)

### What are Local Zones?

**Local Zones** are AWS infrastructure deployments that place AWS compute, storage, database, and other resources **closer to large population and industry centers**.

### Key Features:
- Serve local users with **low-latency** communications
- Support **AWS Direct Connect** connections
- Code for a Local Zone is **Region code + identifier** indicating physical location
  - Example: `us-west-2-lax-1` (Los Angeles)

### Availability:
- Available in **35 metropolitan areas** around the world
- **18 in the US**, **17 outside the US** (as of now)
- Available in India, as well as other millionaire-digit cities

### Use Case Example:
**Couchbase** reduces latency by **80%** for distributed database solutions using AWS Local Zones, bringing virtual workstations closer to artists and content creators.

---

## 6. AWS Wavelength (Optional)

### What is AWS Wavelength?

AWS Wavelength enables developers to build applications that require **ultra-low latency** infrastructure to deliver low latency to **mobile devices and end users**.

### How It Works:
- Embeds AWS compute and storage directly inside the **5G network infrastructure**
- A **Carrier Gateway** provides connectivity to the carrier network
- Reduces latency for 5G users
- Eliminates multiple network hops between 5G networks and AWS services

### Architecture:
- Infrastructure is deployed **inside communications service providers' (CSP) networks**
- Extends the VPC to one or more Wavelength Zones
- Resources deployed in **Wavelength Subnets**

### Key Characteristics:
- A **Wavelength Zone** is an isolated zone in the carrier location where the infrastructure is deployed
- Tied to a Region (identified by an identifier indicating physical location)
  - Example: `us-east-1-wl1-bos-wlz-1` (Boston)
- **Not available in all regions**
- Currently limited to specific locations

### Purpose:
Enables developers to build and deploy applications that require ultra-low latency to mobile devices and users connected to the 5G network.

### Use Cases:
- Applications that provide **industrial robots**
- **Smart factories** requiring real-time analysis
- **Mobile gaming**
- **Video streaming** requiring highly responsive experiences for 5G users

### Reference Project:
[AWS Wavelength Enabled Application Example](https://aws.amazon.com/blogs/compute/deploying-your-first-5g-enabled-application-with-aws-wavelength/)

---

## 7. AWS Outposts (Optional)

### What are AWS Outposts?

An **Outpost** is a pool of AWS compute and storage capacity deployed at a **customer site** for:
- Lower latency
- Local data processing needs

### How It Works:
- AWS operates, monitors, and manages the infrastructure
- Physically installed, fully-managed compute and storage racks
- A **logical extension** of your AWS Region
- Must run workloads on-premises due to latency or data residency requirements

### Use Cases:
- Applications that need to run **physically local**
- Seamless connectivity to other AWS services
- Industries like **healthcare** and **smart factories**

### Architecture:
Applications connect to outposts in **customer premises**, which connect back to the AWS Region.

---

## 8. Global vs Regional AWS Services

### Global Services (Single Configuration):
These services operate across **all AWS regions** with a single configuration:

- **IAM**: User/Role management
- **Route 53**: DNS routing
- **CloudFront**: CDN
- **WAF**: Security

### Regional Services:
These services are **specific to AWS regions** and must be configured per region:

- **EC2**: Compute
- **Lambda**: Serverless
- **Elastic Beanstalk**: PaaS
- **Rekognition**: Image/Video AI

---

## 9. AWS Shared Responsibility Model

### Overview
**Security and Compliance** is a shared responsibility between AWS and the customer.

### AWS Responsibility: "Security OF the Cloud"
AWS is responsible for protecting the **infrastructure** that runs all AWS services:

- **Hardware**: Physical data centers, servers, storage devices
- **Software**: Hypervisors, networking software
- **Networking**: Network infrastructure
- **Facilities**: Physical security of data centers

### Customer Responsibility: "Security IN the Cloud"
Customer responsibility is determined by the **AWS Cloud services** they select:

#### Customer Responsibilities:
- **Platform, Applications, Identity & Access Management**
- **Operating System, Network & Firewall Configuration**
- **Client-side Data Encryption & Data Integrity**
- **Server-side Encryption** (File system and/or data)
- **Network Traffic Protection** (Encryption, integrity, identity)

#### Shared Controls:
- **Patch Management**
- **Configuration Management**
- **Awareness & Training**

### Visual Breakdown:

```
┌─────────────┬──────────────────────────────────────────────────┐
│  CUSTOMER   │ Customer Data                                    │
│             │ Platform, Applications, IAM                      │
│RESPONSIBLE  │ OS, Network & Firewall Configuration             │
│    FOR      │ Client-side & Server-side Encryption             │
│ SECURITY IN │ Network Traffic Protection                       │
│  THE CLOUD  │                                                  │
├─────────────┼──────────────────────────────────────────────────┤
│             │  SOFTWARE                                        │
│    AWS      │  Compute | Storage | Database | Networking       │
│RESPONSIBLE  │                                                  │
│    FOR      │  HARDWARE or AWS GLOBAL INFRASTRUCTURE           │
│ SECURITY OF │  Regions | AZs | Edge Locations                  │
│  THE CLOUD  │                                                  │
└─────────────┴──────────────────────────────────────────────────┘
```

### Reference:
[AWS Shared Responsibility Model Documentation](https://aws.amazon.com/compliance/shared-responsibility-model/)

---

## Key Takeaways

1. **AWS Regions** provide geographic isolation and data sovereignty
2. **Availability Zones** enable high availability and fault tolerance within regions
3. **Edge Locations** reduce latency through content caching and DNS services
4. **Local Zones** bring AWS services closer to specific metropolitan areas
5. **Wavelength** enables ultra-low latency for 5G mobile applications
6. **Outposts** extend AWS infrastructure to customer premises
7. **Global vs Regional services** - understand which services work across all regions
8. **Shared Responsibility Model** - security is shared between AWS and customers

---

**Progress**: Week 1 of 52 ✓