# AWS EC2 \& Compute – Comprehensive DevOps Notes

---


## Lesson 33. Amazon Compute

### What is Amazon Compute?

When you think of compute in the cloud, you're essentially thinking about the power behind running your applications. In traditional setups or on-premises environments, this would be physical servers in a data centre, but in the cloud, AWS handles the physical infrastructure while you focus on what you want those servers to actually do.

### AWS Compute Categories

### EC2 (Elastic Compute Cloud)

**Classic Virtual Machines:** Think of EC2 as your traditional VMs or virtual machines. You have complete control over the operating system, software, and configuration. This provides maximum flexibility for your computing needs.

### Containers

**Lightweight Application Packaging:** Containers are essentially a way to package everything your application needs (code, libraries, dependencies) into a neat, organised bundle.

**Two Main Container Services:**

- **ECS (Elastic Container Service):** Amazon's own container orchestration service
- **EKS (Elastic Kubernetes Service):** For teams who prefer using Kubernetes


### Serverless (Lambda)

**No Server Management:** Serverless might sound like magic, and in many ways it is. With Lambda, you don't worry about servers at all. AWS automatically runs your code when it's triggered and scales automatically.

**Pay-Per-Use Model:** You only pay for the compute time your code actually uses, like renting a server by the millisecond.

### High Availability and Scalability

**Universal AWS Concepts:** AWS offers high availability and scalability across all compute options, whether you're using EC2, containers, or serverless functions. These concepts are fundamental to cloud computing and DevOps practices.

**Importance:** Understanding high availability and scalability is crucial because they form the foundation of reliable, robust cloud architectures.

---


## Lesson 34. Amazon EC2

### What is EC2?

**EC2 (Elastic Compute Cloud)** is part of AWS's Infrastructure as a Service (IaaS) offering. Essentially, you're renting virtual machines or servers from AWS. The key word here is "renting" because you pay only for what you use.

### Why EC2 is Important

**Most Popular AWS Service:** EC2 is extremely popular because of its flexibility. Whether you're a startup or a large enterprise, you can scale up or down as needed and only pay for actual usage.

### Core EC2 Capabilities

### Renting Virtual Machines

**Primary Function:** You can spin up virtual machines, choose the operating system, and configure them based on your specific requirements.

### Data Storage with EBS

**Virtual Hard Drives:** You need somewhere to store your data alongside your virtual machines. EBS (Elastic Block Store) provides this functionality, essentially acting like a hard drive for your EC2 instances.

### Load Balancing with ELB

**Traffic Distribution:** When you have multiple EC2 instances running simultaneously, you need to ensure traffic is distributed evenly. ELB (Elastic Load Balancer) helps distribute incoming requests across your instances, preventing one machine from being overloaded while others remain idle.

### Auto Scaling with ASG

**Automatic Scaling Magic:** ASG (Auto Scaling Group) is the feature that allows EC2 to scale automatically. When your application experiences increased traffic, more instances are automatically added. When traffic decreases, extra instances are removed. This ensures you only pay for what you actually use.

### Fundamental Learning Value

Understanding EC2 is essential for grasping how cloud computing works, especially with AWS. The concepts of virtual machines, scaling, and load balancing are key ideas you'll encounter repeatedly in cloud architecture.

---


## Lesson 35. EC2 Sizing \& Configuration Options

### Operating System Selection

**OS Options:** You can choose from various operating systems including Linux, Windows, macOS, and many others. Your choice depends on what your application requires or what you're comfortable managing.

### Compute Power Configuration

**CPU Selection:** You decide how much processing power you need, which essentially means choosing CPU cores. Consider whether you need basic processing power or something more substantial for tasks like machine learning models or big data processing.

### Memory (RAM) Configuration

**RAM Selection:** You select how much memory your instance will have. More memory helps with handling larger amounts of data in real-time and running bigger applications smoothly.

### Storage Options

### Network Attached Storage

**EBS and EFS Options:**

- **EBS (Elastic Block Store):** Functions like a hard drive attached to your virtual machine
- **EFS (Elastic File System):** Provides shared storage accessible from multiple instances


### Hardware Storage

**EC2 Instance Store:** This is hardware-level storage physically attached to the host machine. It's very fast but temporary, meaning if you stop the instance, you lose all data stored on it.

### Networking Configuration

### Network Card Speed

**Traffic Capacity:** You can configure the network card speed depending on how much traffic you expect your instance to handle.

### Public IP Address

**Internet Accessibility:** You can assign a public IP address if you want your instance to be accessible from the internet.

### Security Configuration

### Firewall Rules (Security Groups)

**Traffic Control:** Security Groups act as firewalls for your instance. You can set up rules to control who can access your instance and which types of traffic can get through. This is extremely important for securing your EC2 instances.

### Bootstrap Script (EC2 User Data)

**Automatic Setup:** This is a script that runs automatically when the instance launches for the first time. You can use it to install software, run updates, or perform setup tasks immediately when the instance starts.

### Configuration Importance

Taking time to properly configure these options based on your application needs is crucial. Wrong sizing can lead to poor performance or overpaying for resources you don't actually need.

---


## Lesson 36. EC2 User Data

### What is EC2 User Data?

When you launch an EC2 instance, you can provide user data, which is essentially a script that runs automatically when the instance starts up for the first time. This provides an excellent way to bootstrap your instance by running commands or tasks immediately when the machine starts.

### Common User Data Tasks

### Installing Updates

**System Maintenance:** You can automatically ensure your instance is fully up to date with the latest security patches. The user data script handles this automatically without manual intervention.

### Software Installation

**Automated Application Setup:** Instead of manually installing software like Nginx or Apache on your instance, you can have the user data script handle everything automatically at launch time.

### File Downloads

**Resource Retrieval:** Download common packages, configuration files, or even your application code from the internet. Essentially, any automation task you'd want to run when your machine first starts up can be included here.

### User Data Characteristics

### One-Time Execution

**Setup Focus:** User data is designed specifically for setup tasks. Once the instance is running, the script won't run again unless you stop and start the instance with new user data.

### Root Privileges

**System Access:** EC2 user data scripts run with root privileges, meaning they have complete control over the system. This is powerful but requires careful consideration of what you include in the script.

### DevOps Benefits

**Time Saving:** User data is invaluable for DevOps professionals because it eliminates the need to manually log into every instance to run setup commands. In larger production environments, manual setup would be completely impractical.

**Automated Deployments:** You configure the setup once, and AWS handles the rest, making it perfect for automated deployments and consistent environment creation.

---


## Lesson 37. EC2 User Data Demo

### Instance Creation Process

### Basic Setup

1. **Access EC2 Console:** Log into your AWS account and navigate to EC2
2. **Launch Instance:** Click "Launch Instance" to begin the setup process
3. **Instance Naming:** Provide a descriptive name for your instance

### Configuration Steps

4. **AMI Selection:** Choose Amazon Linux Image (keep as default)
5. **Architecture:** Select 64-bit instance type
6. **Instance Type:** Choose t2.micro (free tier eligible)

### Security Configuration

7. **Key Pair Creation:** Create a new key pair for secure access
8. **Key Pair Details:** Choose RSA encryption and .pem format for the private key file
9. **Key Pair Storage:** Save the key pair securely, as you'll need it for SSH access

### Network Settings

10. **VPC Configuration:** Use the default VPC created automatically
11. **Public IP:** Enable auto-assign public IP
12. **Security Groups:** Allow SSH traffic with appropriate IP restrictions
13. **Storage:** Keep default settings with "delete on termination" enabled

### SSH Access Process

**Connection Command:** Use SSH with your key pair to connect to the instance
**Authentication:** The command structure is: `ssh -i [key-pair-file] ec2-user@[public-ip]`
**Permission Issues:** You may need to modify key pair permissions using `chmod 400 [key-pair-name]`

### Important Cleanup

**Cost Management:** Always terminate instances when finished to avoid unnecessary charges
**Key Pair Management:** Delete unused key pairs for security
**Complete Cleanup:** Remove both the instance and associated key pairs when done

---


## Lesson 38. EC2 Instance Types Overview

### Instance Type Categories

### General Purpose

**Versatile Workloads:** These are well-rounded instances suitable for various use cases including web servers, small databases, and general workloads. They provide a balanced mix of computing resources.

### Compute Optimised

**Processing Power:** When you need substantial processing power, these instances provide extra CPU for tasks like heavy calculations, batch processing, or high-performance computing applications.

### Memory Optimised

**RAM-Intensive Applications:** When your application requires significant memory or RAM, these instances are ideal for in-memory databases, big data processing, or high-performance computing workloads.

### Storage Optimised

**High-Throughput Storage:** Designed for fast and high-throughput storage access. Perfect for large datasets or databases requiring quick storage access.

### Accelerated Computing

**Specialised Processing:** Features GPUs and FPGAs for demanding tasks like machine learning, video processing, or scientific simulations.

### HPC Optimised

**High Performance Computing:** Designed for intensive computing tasks requiring powerful processing and fast networking capabilities.

### Instance Naming Convention

Understanding AWS naming helps you choose the right instance type.

**Example: m5.2xlarge**

- **M:** Instance class (general purpose)
- **5:** Generation number (higher numbers indicate newer, more efficient versions)
- **2xlarge:** Size within the instance class (ranges from small to 32xlarge)


### Instance Class Letters

- **M:** General purpose
- **C:** Compute optimised
- **R:** Memory optimised
- **T:** General purpose (burstable)


### Size Scaling

**Resource Allocation:** Larger sizes provide more CPU, memory, and other resources, but cost more accordingly.

### Selection Strategy

Choosing the right instance type requires balancing your application's needs with your budget. Too small means poor performance, too large means paying for unused resources.

---


## Lesson 38a. Running a Webserver on EC2 Instance Demo

### Instance Launch Process

### Basic Configuration

1. **EC2 Console Access:** Navigate to EC2 console and click "Launch Instance"
2. **Instance Details:** Name your instance (e.g., "first-instance") and set quantity to 1
3. **Operating System:** Select Amazon Linux with free tier eligible AMI
4. **Architecture:** Choose 64-bit (x86) architecture

### Instance Specifications

5. **Instance Type:** Select t2.micro (free tier for one month)
6. **Key Pair Setup:** Create new key pair named "key-pair-1"
7. **Key Format:** Choose RSA type and .pem format (unless using Windows 7/8, then choose .ppk)

### Network Configuration

8. **VPC Settings:** Use default VPC with auto-assign public IP enabled
9. **Security Groups:** Enable SSH traffic and HTTP traffic
10. **Access Control:** Set source to 0.0.0.0/0 for public access

### Storage and Advanced Settings

11. **Storage Volume:** Keep default settings with "delete on termination" enabled
12. **User Data Script:** In advanced details, add the following bootstrap script:
```bash
#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>Hello World from $(hostname -f)</h1>" > /var/www/html/index.html
```


### Script Explanation

- \#!/bin/bash: Specifies the script interpreter
- **yum update -y:** Updates the system automatically
- **yum install -y httpd:** Installs Apache HTTP server
- **systemctl start httpd:** Starts the web server service
- **systemctl enable httpd:** Enables automatic startup
- **echo command:** Creates a basic HTML page with hostname


### Accessing the Webserver

13. **Instance Launch:** Click "Launch Instance" and wait for the instance to become available
14. **Public IP:** Copy the public IP address from the instance details
15. **Web Access:** Navigate to `http://[public-ip]` in your browser
16. **Expected Result:** You should see "Hello World from [private-ip]" displayed

### Important Notes

**HTTPS vs HTTP:** The webserver uses HTTP (port 80), so you must use `http://` in the URL, not `https://`
**Dynamic IP:** If you stop and restart the instance, the public IP will change
**Security Groups:** The instance should have ports 22 (SSH) and 80 (HTTP) open

### Cleanup Process

17. **Stop/Terminate:** Use the AWS console to stop or terminate the instance
18. **Cost Management:** Always clean up resources to avoid unexpected charges

This demonstrates how to provision an Apache webserver on EC2 using user data for automated setup.

---


## Lesson 45. EC2 Instances Purchasing Options

### On-Demand Instances

**Flexible Pricing:** Great for short-term or unpredictable workloads where you want predictable pricing without long-term commitments. You pay by the second, making it flexible but not always the cheapest option.

**Use Cases:** Ideal for testing new applications or running temporary projects where you need immediate access without planning ahead.

### Reserved Instances

**Long-Term Commitments:** Available for one-year or three-year terms, with longer commitments offering better discounts. You commit to using specific instance types in exchange for significant cost savings.

**Two Types:**

- **Standard Reserved Instances:** Best for longer, predictable workloads
- **Convertible Reserved Instances:** Provide flexibility to change instance types over time while maintaining the benefits of the long-term contract

**Use Cases:** Perfect for production applications that you know will run consistently for extended periods.

### Savings Plans

**Flexible Commitments:** Similar to Reserved Instances but with more flexibility. Available for one and three-year terms, they provide discounts for committing to a certain amount of usage across different instance types and regions.

**Benefits:** Offers long-term savings without the restriction of sticking to one specific instance type, providing more operational flexibility.

### Spot Instances

**Bid for Unused Capacity:** Let you bid for unused EC2 capacity at significantly lower prices. However, AWS can reclaim these instances when they need the capacity, making them less reliable.

**Use Cases:** Ideal for workloads that can tolerate interruptions, such as batch processing, data analysis, or other fault-tolerant applications.

**Cost Savings:** Can provide substantial cost reductions but require applications designed to handle sudden termination.

### Dedicated Hosts

**Complete Hardware Control:** You book an entire physical server, giving you full control and visibility over the underlying hardware. This provides the highest level of control and isolation.

**Use Cases:** Necessary for specific compliance requirements or software licensing needs that require dedicated physical hardware.

### Dedicated Instances

**Hardware Isolation:** Ensures no other AWS customers share the underlying hardware with you, providing isolation without the complexity of managing the physical server.

**Use Cases:** Useful when you need isolated hardware for security or compliance reasons but don't require full control over the physical server.

### Capacity Reservations

**Guaranteed Availability:** Reserve capacity in a specific Availability Zone for a certain duration, ensuring resources are available when you need them.

**Use Cases:** Critical workloads that must run in specific locations, especially during high-demand periods when capacity might otherwise be unavailable.

### Cost Optimisation Strategy

**Workload Analysis:** For predictable workloads, Savings Plans or Reserved Instances can provide significant long-term savings. For experimental or flexible needs, On-Demand instances offer the best balance of cost and flexibility.

**Mixed Approach:** Many organizations use a combination of purchasing options to optimize costs across different types of workloads.

---


## Lesson 46. EC2 Instances Purchasing Options - Console Overview

### Spot Requests

**Creating Spot Requests:** Through the EC2 console, you can create spot fleet requests by specifying your requirements including the AMI you want, capacity needs, networking requirements, instance type preferences, and allocation strategy. AWS provides pricing estimates based on your specifications.

### Savings Plans

**Plan Management:** The console allows you to explore different savings plan options, compare costs, and purchase plans that match your usage patterns and budget requirements.

### Reserved Instances

**Purchase Interface:** You can directly purchase Reserved Instances through the console, setting the instance type, payment options, and other specifications that match your needs.

### Dedicated Hosts

**Host Allocation:** The console provides options to allocate dedicated hosts for your specific requirements, giving you control over the physical hardware your instances run on.

### Capacity Reservations

**Reservation Management:** You can create and manage capacity reservations to ensure resource availability in specific Availability Zones.

### Instance Type Explorer

**Type Comparison:** The console includes an instance type finder that helps you identify the right instances for your specific needs.

**Search Functionality:** You can search by category (like machine learning), performance requirements, or specific instance families (M3, T2, etc.) to find instances that match your workload requirements.

**Detailed Specifications:** The interface provides comprehensive information about each instance type, including CPU, memory, storage, and networking capabilities.

### Practical Usage

**Research Tool:** Use the console to research different instance types and pricing options before making purchasing decisions.

**Cost Planning:** The pricing information and calculators help you plan your AWS costs based on different purchasing strategies.

**Resource Management:** The console provides centralized management for all your EC2 purchasing options and reservations.

This comprehensive overview of purchasing options helps you make informed decisions about the most cost-effective way to run your workloads on AWS.

## EC2 Key Takeaways

### Core Concepts

- **EC2 provides virtual machines** with complete control over operating system and configuration
- **User Data scripts** automate instance setup and software installation
- **Instance types** are optimized for different workloads (compute, memory, storage, etc.)
- **Security Groups** act as virtual firewalls controlling network access


### Configuration Flexibility

- **Multiple operating systems** supported (Linux, Windows, macOS)
- **Scalable resources** from small instances to high-performance computing
- **Storage options** include temporary instance store and persistent EBS volumes
- **Network configuration** includes public/private IP addressing and security controls


### Cost Management

- **Multiple purchasing options** from flexible on-demand to cost-effective reserved instances
- **Auto Scaling Groups** automatically adjust capacity based on demand
- **Spot instances** provide significant savings for fault-tolerant workloads
- **Proper instance sizing** prevents both performance issues and overspending


### Best Practices

- **Always terminate instances** when finished to avoid unnecessary charges
- **Use appropriate instance types** based on your specific workload requirements
- **Implement proper security** through Security Groups and key pair management
- **Automate setup tasks** using User Data scripts for consistency and efficiency


### Real-World Applications

- **Web servers** hosting applications and websites
- **Development and testing** environments with flexible scaling
- **Batch processing** and data analysis workloads
- **High-performance computing** for scientific and machine learning applications

EC2 forms the foundation of AWS compute services, providing the flexibility and control needed for virtually any computing workload while offering various pricing models to optimize costs based on your specific requirements.

These comprehensive EC2 \& Compute notes cover all the essential information from your transcripts while maintaining the clear, beginner-friendly format you requested, using analogies only where truly beneficial for understanding complex concepts.


