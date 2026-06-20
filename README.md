# Full Revision Notes (Chapter 1 – Chapter 8)

**Module: Designing and Developing Applications on the Cloud (DDAC)**

---

# Chapter 1: Introduction to Cloud Computing (Part 1)

## 1. What is Cloud Computing?

Cloud computing means using IT resources (servers, storage, databases, software, networking) through the internet instead of owning and managing physical hardware.

### Traditional Computing

* Buy physical servers and equipment.
* Need server room, electricity, cooling, and security.
* High upfront cost.
* Difficult to increase capacity quickly.

### Cloud Computing

* Resources are provided online.
* Pay only for what you use.
* Easy to scale up or down.
* No need to maintain hardware.

---

## 2. Characteristics of Cloud Computing

### On-Demand Self-Service

Users can get resources whenever needed without contacting the provider.

### Broad Network Access

Services can be accessed through the internet from many devices.

### Resource Pooling

Many customers share the same cloud infrastructure.

### Rapid Elasticity

Resources can increase or decrease quickly.

### Measured Service

Usage is monitored and charged based on consumption.

---

## 3. Cloud Service Models

### Infrastructure as a Service (IaaS)

Provider manages:

* Hardware
* Networking
* Storage

Customer manages:

* Operating system
* Applications
* Data

**Example:** Amazon EC2

---

### Platform as a Service (PaaS)

Provider manages:

* Hardware
* Operating system
* Runtime environment

Customer manages:

* Applications
* Data

**Example:** AWS Elastic Beanstalk

---

### Software as a Service (SaaS)

Provider manages everything.

Users only use the software.

**Examples:**

* Gmail
* Microsoft 365
* Google Docs

---

## 4. Cloud Deployment Models

### Public Cloud

* Available to everyone.
* Managed by cloud provider.

Example:

* AWS
* Azure
* Google Cloud

### Private Cloud

* Used by one organization only.
* More control and security.

### Hybrid Cloud

* Combination of public and private cloud.

### Multi-Cloud

* Uses multiple cloud providers.

---

## 5. Advantages of Cloud Computing

### Trade Capital Expense for Variable Expense

No need to buy expensive hardware.

### Massive Economies of Scale

Cloud providers serve many customers and reduce costs.

### Stop Guessing Capacity

Scale resources when needed.

### Increase Speed and Agility

Deploy resources within minutes.

### Reduce Data Center Costs

No need to maintain physical servers.

### Go Global Quickly

Deploy services worldwide easily.

---

# Chapter 2: Introduction to Cloud Computing (Part 2)

## 1. History of Cloud Computing

### Evolution Stages

1. Mainframe Computing
2. Client-Server Computing
3. Grid Computing
4. Cloud Computing

---

## 2. Grid Computing vs Cloud Computing

### Grid Computing

* Uses multiple computers together.
* Focuses on sharing computing power.

### Cloud Computing

* Provides services through internet.
* More flexible and scalable.

---

## 3. Virtualization

### Definition

Virtualization allows one physical machine to run multiple virtual machines (VMs).

Benefits:

* Better resource utilization
* Lower cost
* Easier management

---

## 4. Types of Virtualization

### Server Virtualization

One physical server runs many virtual servers.

### Network Virtualization

Creates virtual networks.

### Storage Virtualization

Combines storage devices into one storage pool.

### Desktop Virtualization

Desktop runs on a remote server.

### Application Virtualization

Applications run separately from the operating system.

---

## 5. Hypervisors

Software that creates and manages virtual machines.

### Type 1 (Bare-Metal)

Runs directly on hardware.

Examples:

* VMware ESXi
* Hyper-V

### Type 2 (Hosted)

Runs on an operating system.

Examples:

* VirtualBox
* VMware Workstation

---

## 6. AWS Global Infrastructure

### Region

Physical geographic area.

Examples:

* Singapore
* Tokyo
* London

Choose a region based on:

* Cost
* Compliance
* Distance from users
* Service availability

---

### Availability Zone (AZ)

One or more data centers within a region.

Benefits:

* High availability
* Fault tolerance

---

### Edge Location

Used to deliver content faster to users.

Example:

* Amazon CloudFront

---

# Chapter 3: Cloud Development Phases and Assisted Tools

## 1. Systems Development Life Cycle (SDLC)

A structured process for developing software.

### Main Phases

#### Planning

Define project goals.

#### Analysis

Gather requirements.

#### Design

Create system design.

#### Development

Write code.

#### Testing

Find and fix bugs.

#### Deployment

Release the system.

#### Maintenance

Improve and support the system.

---

## 2. SDLC Methodologies

### Waterfall

* Linear process.
* Each phase completed before next phase.

### Agile

* Development in small iterations.
* Faster feedback.
* Flexible changes.

---

## 3. Getting Started with AWS

### Create AWS Account

Need:

* Email
* Payment method

---

### Configure IAM Permissions

Create:

* Users
* Groups
* Roles

---

### Setup Development Environment

Tools:

* AWS Console
* AWS CLI
* AWS Cloud9

---

## 4. AWS Cloud9

Cloud-based IDE.

Features:

* Write code online
* Debug applications
* Run code directly

Benefits:

* No installation needed
* Accessible anywhere

---

## 5. AWS CLI

Command Line Interface used to manage AWS services through commands.

Example:

```bash
aws s3 ls
```

---

## 6. AWS SDK

Software Development Kit used in programming languages.

Examples:

* Java
* Python
* JavaScript
* C#

Benefits:

* Easier integration with AWS services
* Faster development

---

## 7. AWS Service Categories

### Compute

Example:

* EC2
* Lambda

### Storage

Example:

* S3
* EBS

### Database

Example:

* RDS
* DynamoDB

### Networking

Example:

* VPC
* CloudFront

### Security

Example:

* IAM

---

# Chapter 4: Securing Access to Cloud Resources

## 1. Shared Responsibility Model

### AWS Responsibilities

Security **of** the cloud:

* Hardware
* Networking
* Data centers
* Physical security

### Customer Responsibilities

Security **in** the cloud:

* Data
* Applications
* User accounts
* Permissions

---

## 2. Identity and Access Management (IAM)

IAM controls who can access AWS resources.

---

## 3. Authentication

Verifies identity.

Methods:

* Username
* Password
* Access Key
* MFA

---

## 4. Multi-Factor Authentication (MFA)

Requires:

1. Password
2. Additional verification code

Benefits:

* Stronger security
* Prevents unauthorized access

---

## 5. Authorization

Determines what actions a user can perform.

Examples:

* Read data
* Create resources
* Delete resources

---

## 6. IAM Policies

JSON documents that define permissions.

Policies specify:

* Allow
* Deny
* Actions
* Resources

---

## 7. Types of Policies

### Identity-Based Policy

Attached to users, groups, or roles.

### Resource-Based Policy

Attached directly to resources.

---

## 8. IAM Groups

Collection of users.

Benefits:

* Easier permission management.

---

## 9. IAM Roles

Temporary permissions.

Used by:

* Applications
* AWS services
* Cross-account access

---

## 10. Principle of Least Privilege

Give users only the permissions they need.

Benefits:

* Better security
* Reduced risk

---

# Chapter 5: Compute Solutions in Cloud (Part 1)

## 1. Compute Services

Provide processing power for applications.

Examples:

* EC2
* Lambda
* Elastic Beanstalk

---

## Categorizing compute services

| Services                                              | Key Concepts                                                                   | Characteristics                                                                                                                     | Ease of Use                                                                                      |
| ----------------------------------------------------- | ------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| Amazon EC2                                            | - Infrastructure as a Service (IaaS)<br>- Instance-based<br>- Virtual machines | - Provision virtual machines that you can manage as you choose                                                                      | A familiar concept to many IT professionals.                                                     |
| AWS Lambda                                            | - Serverless computing<br>- Function-based<br>- Low-cost                       | - Write and deploy code that runs on a schedule or that can be triggered by events<br>- Use when possible (architect for the cloud) | A relatively new concept for many IT staff members, but easy to use after you learn how.         |
| Amazon ECS<br>Amazon EKS<br>AWS Fargate<br>Amazon ECR | - Container-based computing<br>- Instance-based                                | - Spin up and run jobs more quickly                                                                                                 | AWS Fargate reduces administrative overhead, but you can use options that give you more control. |
| AWS Elastic Beanstalk                                 | - Platform as a Service (PaaS)<br>- For web applications                       | - Focus on your code (building your application)<br>- Can easily tie into other services—databases, Domain Name System (DNS), etc.  | Fast and easy to get started.                                                                    |

---

## 2. Amazon EC2

Elastic Compute Cloud.

Provides virtual servers in AWS.

Benefits:

* Flexible
* Scalable
* Pay-as-you-go

---

## 3. Components of EC2

### AMI (Amazon Machine Image)

Template used to launch instances.

Contains:

* Operating system
* Software
* Configuration

---

### Instance Type

Defines:

* CPU
* Memory
* Storage
* Network performance

---

### Network Settings

Control network connectivity.

---

### IAM Role

Allows EC2 to access AWS services securely.

---

### User Data Script

Runs automatically when instance starts.

---

### Storage Options

Examples:

* EBS
* Instance Store

---

### Tags

Labels for resources.

Example:

* Name=WebServer

---

### Security Group

Virtual firewall.

Controls:

* Inbound traffic
* Outbound traffic

---

### Key Pair

Used for secure login.

Contains:

* Public key
* Private key

---

## 4. EC2 Instance Lifecycle

States:

1. Pending
2. Running
3. Stopping
4. Stopped
5. Rebooting
6. Terminated

---

## 5. Elastic IP

Static public IP address.

Useful when instance restarts.

---

## 6. EC2 Metadata

Information about the running instance.

Examples:

* Instance ID
* IP address

---

## 7. Amazon CloudWatch

Monitoring service.

Tracks:

* CPU usage
* Memory
* Network activity

---

# Chapter 6: Compute Solutions in Cloud (Part 2)

## 1. AWS Elastic Beanstalk

Platform as a Service (PaaS).

Makes application deployment easier.

Supports:

* Java
* Python
* PHP
* Node.js
* .NET

---

## 2. How Elastic Beanstalk Works

Developer uploads code.

Elastic Beanstalk automatically:

* Creates EC2 instances
* Configures load balancing
* Handles scaling
* Monitors application

---

## 3. Benefits

### Easy Deployment

No need to configure infrastructure manually.

### Automatic Scaling

Handles traffic changes.

### Monitoring

Integrated with CloudWatch.

### Faster Development

Focus on code instead of infrastructure.

---

## 4. What You Can Control

* Application code
* Environment variables
* Instance type
* Scaling settings

AWS controls:

* Infrastructure management
* Provisioning
* Maintenance

---

# Chapter 7: Database Solutions in Cloud

## 1. Cloud Databases

Databases hosted in the cloud.

Benefits:

* Scalability
* High availability
* Easy management
* Backup and recovery

---

## 2. Types of Databases

### Relational Database (SQL)

Stores data in tables.

Examples:

* MySQL
* PostgreSQL
* Oracle

---

### NoSQL Database

Stores non-tabular data.

Examples:

* DynamoDB
* MongoDB

---

## 3. Amazon RDS

Managed relational database service.

Benefits:

* Automatic backups
* Patching
* Monitoring
* High availability

---

## 4. Multi-AZ Deployment

Creates standby database in another Availability Zone.

Benefits:

* Failover support
* Higher availability

---

## 5. Read Replicas

Copies of the main database.

Benefits:

* Improve read performance
* Reduce workload

---

## 6. When to Use RDS

Use when:

* Structured data
* SQL queries
* ACID transactions

---

## 7. NoSQL Databases

Designed for:

* Large scale applications
* Flexible data structures

Benefits:

* Fast performance
* High scalability

---

## 8. Types of NoSQL Databases

### Key-Value Database

Stores:

* Key
* Value

Example:
UserID → Name

---

### Document Database

Stores JSON-like documents.

---

### Column Database

Stores data by columns.

---

### Graph Database

Stores relationships between data.

---

## 9. Amazon DynamoDB

Fully managed NoSQL database.

Benefits:

* Serverless
* Fast
* Scalable

---

## 10. DynamoDB Components

### Table

Collection of data.

### Item

Single record.

### Attribute

Data field.

---

## 11. Primary Keys

### Simple Primary Key

Partition Key only.

### Composite Primary Key

Partition Key + Sort Key.

---

## 12. Secondary Indexes

Allow additional query methods.

### Global Secondary Index (GSI)

Different partition key.

### Local Secondary Index (LSI)

Same partition key.

---

## 13. Read Consistency

### Eventually Consistent

Faster but may not show latest data immediately.

### Strongly Consistent

Always returns latest data.

---

## 14. Throughput Modes

### Provisioned

Manually set capacity.

### On-Demand

Automatically scales capacity.

---

# Chapter 8: Storage Solutions in Cloud (Part 1)

## 1. Cloud Storage

Stores data in cloud infrastructure.

Benefits:

* Scalability
* Durability
* Accessibility
* Cost savings

---

## 2. Types of Cloud Storage

### Object Storage

Stores files as objects.

### Block Storage

Stores data in blocks.

### File Storage

Stores data as files and folders.

---

## 3. Amazon S3 (Simple Storage Service)

Object storage service.

Features:

* Highly durable
* Highly scalable
* Secure
* Accessible anywhere

---

## 4. S3 Components

### Bucket

Container for objects.

### Object

Actual file stored in bucket.

Each object contains:

* Data
* Metadata
* Unique identifier

---

## 5. Benefits of S3

* Unlimited scalability
* High durability
* Easy access
* Cost-effective

---

## 6. S3 Storage Classes

Examples:

* S3 Standard
* S3 Intelligent-Tiering
* S3 Standard-IA
* S3 One Zone-IA
* S3 Glacier
* Glacier Deep Archive

Choose based on:

* Access frequency
* Cost
* Retrieval speed

---

## 7. Common S3 Use Cases

* Website hosting
* Backup
* Data archive
* Media storage
* Big data analytics

---

## 8. Block Storage

Stores data in fixed-size blocks.

Suitable for:

* Databases
* Operating systems
* Virtual machines

---

## 9. Amazon EBS (Elastic Block Store)

Block storage used with EC2.

Features:

* Persistent storage
* High performance
* Scalable

---

## 10. EBS Volume Types

### General Purpose SSD (GP)

Balanced performance and cost.

### Provisioned IOPS SSD

High-performance workloads.

### HDD Volumes

Suitable for large sequential workloads.

---

## 11. EBS Snapshots

Backup copies of EBS volumes.

Benefits:

* Disaster recovery
* Data protection
* Easy restoration

---

# Quick Exam Summary

### Cloud Service Models

* IaaS → EC2
* PaaS → Elastic Beanstalk
* SaaS → Gmail

### AWS Infrastructure

* Region = Geographic area
* AZ = Data center(s)
* Edge Location = Fast content delivery

### Security

* IAM controls access
* MFA improves security
* Least Privilege = minimum permissions

### Compute

* EC2 = Virtual server
* Elastic Beanstalk = Easy application deployment

### Database

* RDS = Relational SQL database
* DynamoDB = NoSQL database

### Storage

* S3 = Object Storage
* EBS = Block Storage

These notes cover the main concepts, definitions, features, advantages, components, and AWS services discussed from **Chapter 1 to Chapter 8** in the lecture slides using simplified vocabulary for revision and exam preparation.
