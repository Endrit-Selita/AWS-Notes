# AWS Security Group \& Cloud Networking Basics – Comprehensive DevOps Notes

---

## Lesson 39. Introduction to Security Groups

### What are Security Groups?

**Security Groups (SGs)** are essential for network security in AWS. In simple terms, they control how traffic flows into and out of your EC2 instances, functioning as virtual firewalls that decide what's allowed in and what's allowed out of your instance.

### Core Security Group Principles

### Network Security Backbone

Security groups form the foundation of network security for EC2 instances. Anytime your instance deals with incoming or outgoing traffic, the security group rules define what's permitted.

### Allow Rules Only

Unlike traditional firewalls that can have both allow and deny rules, security groups focus exclusively on what's allowed. Anything that isn't explicitly allowed is blocked by default. This approach simplifies security management by removing the complexity of conflicting allow and deny rules.

### Traffic Control Methods

You can set rules that specify allowed traffic based on:

- **IP addresses:** Define specific IP addresses or ranges that can access your instance
- **Other security groups:** Reference other security groups for dynamic access control

This flexibility is particularly useful in large environments where instances need to communicate with each other but shouldn't be exposed to the public internet.

### Stateful Nature

Security groups are **stateful**, meaning if you allow inbound traffic, the corresponding outbound traffic is automatically allowed, and vice versa. This eliminates the need to create separate rules for response traffic.

### Practical Example

For a website running on EC2, you would create rules that allow inbound traffic on port 80 (HTTP) or port 443 (HTTPS) for web access, but block everything else like SSH access, database access, and other ports. Security groups provide this granular control over your instance's network access.

---


## Lesson 40. Security Groups Deeper Dive

### What Security Groups Regulate

Security groups act as firewalls for instances, but let's examine exactly what they control and how they maintain instance security.

### Port Access Control

**Port Management:** Security groups control which ports are open on your instance. For a web server, you need port 80 open for HTTP traffic, but you wouldn't want every port open as this could expose your instance to unwanted traffic.

### Authorised IP Ranges

**IPv4 and IPv6 Support:** Control who can access your instance based on IP addresses. For SSH access, you might only allow your office IP, home IP, or other trusted IP addresses. Security groups let you define which IP addresses or ranges are permitted.

### Traffic Direction Control

### Inbound Traffic

**Incoming Connections:** This covers traffic coming into your instance, whether it's web requests, SSH connections, or database access. Security groups control what's allowed to enter your instance.

### Outbound Traffic

**Outgoing Connections:** This manages traffic leaving your instance. You can control what your instance is allowed to connect to, such as preventing internet access unless absolutely necessary.

### Security Group Rule Examples

| Type | Protocol | Port Range | Source | Description |
| :-- | :-- | :-- | :-- | :-- |
| HTTP | TCP | 80 | 0.0.0.0/0 | Test http page |
| SSH | TCP | 22 | 122.149.196.85/32 | Moderate |
| Custom TCP Rule | TCP | 4567 | 0.0.0.0/0 | Java app |

### Rule Breakdown

**HTTP Rule:** Uses TCP protocol on port 80, with source 0.0.0.0/0 (open to the world) for general web access.

**SSH Rule:** Uses TCP protocol on port 22, but restricts source to a single IP address (122.149.196.85/32) for secure administrative access.

**Custom TCP Rule:** Demonstrates how you can create rules for specific application ports that your software might use.

### Security Best Practices

Keep your security group rules as restrictive as possible. Only open ports you absolutely need and limit access to trusted IP addresses. This approach minimises your instance's exposure to potential attacks and maintains a strong security posture.

---


## Lesson 41. Security Groups Detailed Workflow

### How Security Groups Work in Practice

Let's examine how security groups function using a detailed workflow example with an EC2 instance.

### The Setup

**EC2 Instance:** You have created an EC2 instance with a specific public IP address. This virtual machine runs on AWS and needs network access control.

**Security Group Attachment:** Every EC2 instance has a security group attached to it (unless you explicitly choose not to attach one). The security group acts like a virtual bouncer, only allowing traffic that matches your predefined rules.

### Traffic Filtering Process

**Rule Matching:** Any incoming request must match the rules you've established. The security group filters traffic based on IP addresses and ports before it reaches your instance.

### Practical Examples

### Authorised SSH Access

**Scenario:** Your computer tries to connect to the EC2 instance on port 22 (SSH).
**Outcome:** Since your computer's IP address is authorised to use port 22, the security group allows this connection, enabling you to securely SSH into your EC2 instance.

### Blocked SSH Attempt

**Scenario:** Another computer with a different IP address attempts to connect to the EC2 instance on port 22.
**Security Response:** This IP address isn't authorised for port 22 access, so the security group blocks the attempt.
**Result:** The unauthorised computer cannot access your instance, maintaining security.

### Outbound Traffic Flow

**Internet Access:** The diagram shows outbound traffic (data going from your instance to the internet). Your EC2 instance can make requests to any IP address on any port unless your outbound rules specify otherwise.

**Default Behaviour:** By default, security groups include an outbound rule allowing all outbound traffic. This enables your instance to download updates or access external APIs.

**Customisation:** You can modify these defaults by removing the default rule and adding specific outbound rules that only allow particular outbound traffic.

### Key Security Principles

**Access Control:** Security groups are fundamentally about controlling access. You decide who can connect (via IP address) and how they can connect (via port).

**Default Deny:** Your EC2 instance stays locked down unless a connection matches your security group rules.

**Layer Protection:** Security groups operate outside the EC2 instance itself, filtering traffic before it reaches your server.

---


## Lesson 42. Security Groups Good to Know

### Security Group Characteristics

### Multi-Instance Attachment

**Reusability:** Security groups can be attached to multiple instances. They're reusable resources, so you can attach the same security group to multiple EC2 instances, making access management across instances much more efficient.

### Regional and VPC Restrictions

**Location Binding:** Security groups are locked to a specific region and VPC combination. You cannot use a security group from one region or VPC in another location. Each security group stays tied to its original location.

### External Operation

**Layer Above Instance:** Security groups operate outside the EC2 instance itself. Think of them as being one layer above the instance. If traffic is blocked by security groups, it won't even reach your instance.

### Troubleshooting Guidelines

### SSH Access Management

**Dedicated SSH Security Group:** Maintain a separate security group specifically for SSH access. This allows you to tightly control which IP addresses can access your instances via SSH without affecting other rules for web traffic or application connections.

### Common Issues and Solutions

### Timeout Problems

**Application Unreachable:** If your application isn't reachable and times out, this usually indicates that your security group is blocking the traffic. This should be your first troubleshooting step when diagnosing connectivity issues.

### Connection Refused Errors

**Internal Application Issues:** If you receive a "connection refused" error, this typically indicates an application or instance problem rather than a security group issue. The traffic is reaching the instance, but the application or service isn't running properly or has configuration problems.

### Default Traffic Behaviour

### Inbound Traffic

**Blocked by Default:** All inbound traffic is blocked by default. You must specifically allow the traffic you want, whether it's HTTP, HTTPS, or SSH access.

### Outbound Traffic

**Allowed by Default:** Unlike inbound traffic, all outbound traffic is authorised by default. Your instance can connect to the internet or other instances unless you create specific rules to block certain connections.

### Practical Troubleshooting Value

Understanding these behaviours dramatically improves troubleshooting speed. Knowing that a timeout usually indicates a security group issue can save significant time when diagnosing connectivity problems. Many access issues stem from incorrect security group configurations rather than application problems.

---


## Lesson 43. Referencing Other Security Groups

### Advanced Security Group Management

Security groups normally define rules using IP addresses, but what happens when you need to control access between instances that might change IP addresses? This is where referencing other security groups becomes invaluable.

### How Security Group Referencing Works

### The Setup

**Primary Instance:** You have an EC2 instance using SG1 to manage its inbound traffic.

**Rule Configuration:** Instead of allowing traffic from specific IP addresses, SG1 references other security groups (SG1, SG2, and SG3) and authorises them to send traffic on specific ports.

### Dynamic Access Control

**Group-Based Permissions:** By referencing SG1, you allow traffic from any instance that has SG1 attached. The same principle applies to SG2 and SG3.

**IP Independence:** This approach eliminates the need to track or update specific IP addresses, as the security group reference automatically includes all instances attached to the referenced groups.

### Practical Benefits

### Simplified Management

**Reduced Administrative Overhead:** Instead of constantly updating IP addresses and manually adjusting firewall rules, you can authorise entire security groups to communicate with each other.

### Microservices Architecture

**Tier-Based Communication:** In a microservices environment, you might want all instances in a database security group to communicate with all instances in an application tier security group. Security group referencing makes this configuration straightforward.

### Dynamic Environment Support

**Auto Scaling Compatibility:** This referencing method is particularly helpful in dynamic environments like auto scaling groups or clusters where instances frequently come and go, but you still need to maintain secure communication between different tiers of your application.

### Configuration Simplicity

**Reference vs IP Management:** Using security groups as references rather than managing individual IP addresses simplifies configuration and reduces the risk of misconfiguration in complex, multi-tier applications.

---


## Lesson 44. Classic Ports to Know

### Essential Network Ports

When configuring security group rules in AWS, you'll frequently need to open or block specific ports. Each port corresponds to a particular service or protocol, and understanding these common ports is crucial for effective network security management.

### Critical Ports for AWS

### SSH (Secure Shell) - Port 22

**Purpose:** Used to securely log into Linux instances for management and administration.
**Security Tip:** Always restrict access to port 22 to only trusted IP addresses to prevent unauthorised access.

### FTP vs SFTP

**FTP (File Transfer Protocol) - Port 21:** Used for uploading files to file shares, but it's not very secure and is being phased out in favour of more secure alternatives.
**SFTP (Secure File Transfer Protocol) - Port 22:** The secure version of FTP that uses SSH, which is why it shares the same port. SFTP is the better option for secure file transfers.

### Web Traffic Ports

**HTTP - Port 80:** Used to access unsecured websites. This handles standard web traffic that doesn't use encryption.
**HTTPS - Port 443:** Used for accessing secure websites with TLS encryption. Essential for websites and applications handling sensitive data as it encrypts all web traffic.

### DNS (Domain Name System) - Port 53

**Function:** Responsible for translating domain names (like google.com) into IP addresses.
**Importance:** Essential for any application that requires domain name resolution.

### Remote Access

**RDP (Remote Desktop Protocol) - Port 3389:** Allows you to log into Windows instances for remote management of Windows-based EC2 instances.

### Additional Important Ports

**SMTP (Simple Mail Transfer Protocol) - Port 25:** Email transmission protocol
**MySQL - Port 3306:** MySQL database connections
**PostgreSQL - Port 5432:** PostgreSQL database connections

### Port Selection Strategy

These represent the most common and important ports you'll encounter in AWS environments. Understanding these ports enables you to configure appropriate security group rules for different types of applications and services.

## Lesson 45. Security Groups Demo

### Practical Security Group Management

Let's examine how to work with security groups through the AWS console interface.

### Accessing Security Groups

**Instance Security:** Each EC2 instance has security groups attached, visible in the security section of the instance details.

**Security Groups Console:** Navigate to the security groups section to see all security groups in your account, including default groups created automatically and custom groups you've created.

### Security Group Components

**Identification:** Each security group has a name and unique ID, similar to EC2 instance IDs.
**Rule Management:** Inbound and outbound rules define what traffic is permitted.

### Modifying Security Group Rules

### Adding Rules

**Rule Types:** You can select from predefined rule types (HTTP, HTTPS, SSH) or create custom rules with specific port numbers.
**Source Configuration:** Rules can allow traffic from anywhere (0.0.0.0/0) or restrict to specific IP addresses.

### Testing Rule Changes

**Immediate Effect:** Security group changes take effect immediately.
**Connectivity Testing:** The demo shows removing an HTTP rule (port 80) and observing that the web server becomes inaccessible, demonstrating the immediate impact of security group modifications.

### Troubleshooting with Security Groups

**Timeout Issues:** When a connection times out (keeps loading indefinitely), this is typically a security group issue where traffic is being blocked.
**Quick Resolution:** Adding the appropriate rule back immediately restores connectivity, confirming that security groups were the cause.

### Outbound Rules Management

**Default Behaviour:** Security groups typically include a default outbound rule allowing all traffic (0.0.0.0/0) to everywhere.
**Internet Access:** This default rule enables EC2 instances to access the internet for downloads, updates, and external API calls.
**Custom Restrictions:** You can remove the default rule and add specific outbound rules for services like DNS (port 53) if you need more restrictive policies.

### Security Best Practices

**Inbound Restrictions:** For inbound rules, it's better to restrict access to only the ports you need to open, and where possible, limit source IPs to trusted addresses.
**IP-Specific Access:** Using "My IP" option restricts access to your current public IP address, providing better security than allowing access from anywhere.

---


## Lesson 46. IPv4 vs IPv6

### Understanding IP Address Formats

IP addresses are essential for identifying devices on networks, and they come in two main formats that serve the same fundamental purpose but with different capabilities.

### IPv4 (Internet Protocol version 4)

**Format:** The older and more common format, appearing as four numbers separated by periods (e.g., 10.16.10.40).
**Number Range:** Each number can be between 0 and 255.
**History:** IPv4 has been around since the 1980s and remains the most widely used format online today.
**Address Capacity:** Allows for 3.7 billion different addresses in the public space.

### IPv6 (Internet Protocol version 6)

**Format:** Looks much more complex than IPv4, using a longer hexadecimal format.
**Development Reason:** Introduced because we're running out of IPv4 addresses, especially with the rise of Internet of Things (IoT) devices.
**Device Growth:** Smart devices like phones, cameras, and even smart fridges need their own IP addresses, creating enormous demand.
**Address Capacity:** IPv6 allows for vastly more addresses, solving the IPv4 scarcity problem.

### Current Usage and Course Focus

**Widespread IPv4 Usage:** Despite IPv6's advantages, IPv4 remains the most common format and easiest to work with, especially when learning networking concepts.

**Growing IPv6 Importance:** IPv6 is becoming increasingly important as the number of connected devices continues growing, but for most practical current use cases, IPv4 remains the primary focus.

### Address Scarcity Challenge

**Original Assumptions:** 3.7 billion IPv4 addresses seemed adequate when first introduced, but demand has skyrocketed with universal device connectivity.

**Future Considerations:** While IPv4 remains dominant for now, understanding that IPv6 represents the future of internet addressing helps in planning for long-term network architecture.

---


## Lesson 47. Private vs Public IP Example

### Network Communication Architecture

This example demonstrates how routers function at layer 3 (network layer) of the OSI model, directing traffic between different networks and enabling communication between private and public network spaces.

### The Network Setup

**Company Networks:** Both Company A and Company B operate their own private networks using private IP addresses, similar to home networks.

**Private IP Limitations:** These private IP addresses aren't routable on the public internet, meaning they cannot communicate directly with external websites or services.

### Internet Gateway Function

**Router Similarity:** The internet gateway functions similarly to your home router, which assigns private IP addresses to devices (like 192.168.0.1 and similar ranges).

**Translation Process:** When you visit a website, your router acts as a middleman, translating private IP addresses into a public IP so traffic can travel over the internet to reach other services.

**Company Implementation:** Each company's internet gateway performs the same function, taking traffic from their private networks and translating it to public IP addresses.

### Network Address Translation (NAT)

**NAT Process:** Both home routers and corporate internet gateways perform Network Address Translation, converting private IPs to public IPs and vice versa.

**Connectivity Enablement:** This translation enables devices in private networks to communicate with the public internet while maintaining internal network security.

### Internet Gateway Importance

**Essential Component:** Without the internet gateway, private networks would remain isolated. Companies wouldn't be able to access websites or services on the public internet.

**Layer 3 Routing:** As discussed in the networking module, layer 3 routers help route traffic between different networks, whether it's home network access to Google or company private network communication with external web servers.

### IP Address Reuse and Uniqueness

**Private IP Reuse:** Private IP addresses can be reused across different networks (both companies can use the same private IP ranges without conflict).

**Public IP Uniqueness:** Public IP addresses must be globally unique, which is why each company receives different public IP addresses when connected to the internet.

**Home Network Parallel:** Just as your home router handles translation between private and public-facing IP addresses, internet gateways provide the same functionality for corporate networks, enabling secure internet connectivity.

---


## Lesson 48. Private vs Public IPv4 Differences

### Fundamental IP Address Types

Understanding the distinction between public and private IP addresses is crucial for networking and security configuration in cloud environments.

### Public IP Addresses

### Internet Identification

**Global Visibility:** A public IP means a machine can be directly identified on the internet, like a website server or your home router's external IP address. It makes the device visible to the world through the internet.

### Global Uniqueness

**Unique Addressing:** Every public IP must be unique across the entire internet. No two devices on the public internet can have the same public IP address simultaneously.

Think of it like a postal address system where no two houses can have exactly the same address and postcode.

### Geolocation Capability

**Location Tracking:** Public IP addresses can often be geo-located quite easily. With a public IP, someone can generally determine what country or even city your machine is located in.

**Commercial Usage:** Websites use this location information for offering localised services or targeted advertisements.

### Private IP Addresses

### Internal Network Usage

**Network-Specific:** Private IP addresses are only used inside private networks like your home or a company's internal network. Devices within that private network can identify each other, but they cannot be seen directly from the internet.

### Limited Uniqueness Requirement

**Local Uniqueness:** While public IP addresses must be unique globally, private IP addresses only need to be unique within their own private network.

**Network Isolation:** Multiple networks can use the same private IP ranges without problems. Your home network's private IP addresses can be identical to mine without causing any conflicts because they exist on separate networks.

### Practical Examples

**Company Networks:** Company A and Company B can both use 192.168.0.1 for their internal devices without any conflict because they operate on completely separate private networks.

**Home Network Parallel:** Your private IP at home might be exactly the same as someone else's private IP in their home network, and this causes no issues because the networks are isolated from each other.

### Security and Access Implications

**Internet Accessibility:** Public IP addresses are directly reachable from the internet, while private IP addresses require network address translation (NAT) through gateways or routers to communicate with external networks.

**Network Segmentation:** This distinction enables network segmentation strategies where internal systems use private addressing for security while maintaining internet connectivity through controlled public IP gateways.

---


## Lesson 49. Elastic IPs

### The Dynamic IP Problem

When you stop and start an EC2 instance, it normally gets assigned a new public IP address. AWS allocates public IP addresses dynamically without guaranteeing that your instance will keep the same one. While this is acceptable in most cases, it can create problems when you need a fixed public IP address.

### What is an Elastic IP?

**Fixed Public Address:** An Elastic IP is a public IPv4 address that you essentially own as long as it's not deleted. You can move it between instances, but it remains under your control regardless of instance state changes.

### How Elastic IPs Work

### Charging Model

**Usage-Based Billing:** Elastic IP addresses are only charged when they're not in use. As long as an Elastic IP is attached to an active instance, there's no additional cost.

**Idle Charges:** However, if you reserve an Elastic IP but don't attach it to anything, AWS will charge you for holding onto unused IP addresses.

### Attachment Rules

**Single Instance Limit:** You can attach an Elastic IP to only one instance at a time, but you can remap it as needed between different instances.

**Flexibility:** This remapping capability is particularly helpful when working with services that need consistent IP addresses, such as web servers or systems with DNS entries pointing to specific addresses.

### Practical Use Cases

### Service Continuity

**External Dependencies:** Elastic IPs are valuable when external services need to point to your instance using a static IP address.

**Web Hosting:** If you're hosting a website or need connections from outside sources, maintaining the same IP address ensures no disruption when restarting instances.

**DNS Stability:** Systems with DNS entries pointing to specific IP addresses benefit from Elastic IP consistency.

### Failure Masking

**Quick Recovery:** You can mask instance or software failures by quickly remapping an Elastic IP to another instance in your account, providing rapid service restoration.

### Usage Recommendations

**Selective Implementation:** If you don't need a fixed public IP address, don't worry about Elastic IPs for development or testing environments.

**Production Considerations:** For production environments where IP consistency is critical, Elastic IPs provide valuable stability and reliability.

---


## Lesson 50. Elastic IP Demo

### Creating and Managing Elastic IPs

### Allocation Process

**IP Address Allocation:** Navigate to Elastic IPs in the EC2 console under Network and Security, then click "Allocate IP address" to receive a random public IP address from AWS's pool for your region.

### Instance Configuration for Elastic IP

**Disable Auto-Assign Public IP:** When creating an instance that will use an Elastic IP, disable the auto-assign public IP setting in the network configuration. This prevents AWS from assigning a random public IP that you'll replace anyway.

### Association Process

**Linking IP to Instance:** Once your instance is running without a public IP, associate your allocated Elastic IP by selecting "Associate IP address" from the Elastic IP actions menu, then choose your target instance from the dropdown.

**Result:** After association, your instance will have the Elastic IP as its public IP address, providing consistent addressing.

### Important Cleanup Procedures

### Cost Management

**Unused IP Charges:** AWS charges for any Elastic IPs that aren't associated with running instances. If an Elastic IP sits unused, you'll incur charges.

### Proper Cleanup Steps

1. **Disassociate:** First, disassociate the Elastic IP from the instance
2. **Release:** Then release the Elastic IP address back to AWS
3. **Instance Termination:** Finally, terminate the instance if no longer needed

### Cost Avoidance

**Billing Prevention:** Following proper cleanup procedures prevents unexpected charges for unused Elastic IP addresses and ensures you're not paying for resources you're not actively using.

---


## Lesson 51. When to Use Elastic IPs

### Appropriate Use Cases

### Failure Recovery

**Quick Instance Switching:** Elastic IPs allow you to mask instance or software failures by rapidly remapping the IP address to another instance in your account, enabling quick traffic switching without downtime.

### Account Limitations

**Default Limit:** You only have five Elastic IPs per account by default, though you can request AWS to increase this limit if needed.

### Why to Avoid Elastic IPs

### Architectural Concerns

**Poor Design Indicator:** Best practice suggests avoiding Elastic IPs unless absolutely necessary, as they often indicate poor architectural decisions. Modern cloud environments offer better alternatives for managing traffic and IP addresses.

### Better Alternatives

### DNS-Based Solutions

**Dynamic DNS:** Instead of relying on Elastic IPs, use a random public IP and register a DNS name to it. This provides a consistent way to connect to your instance without requiring a static IP address.

### Load Balancer Approach

**Superior Alternative:** Load balancers offer more flexibility and reliability for distributing traffic across instances. They don't require public IP addresses and provide better scalability options.

### Modern Architecture Perspective

### Scalability Considerations

**Cloud-Native Design:** Architect with scalability and flexibility in mind. DNS resolution and load balancers align better with modern cloud architecture principles than static IP assignment.

### Band-Aid Solution

**Temporary Fix:** Elastic IPs are often viewed as band-aid solutions in modern cloud architecture. If you find yourself needing many Elastic IPs, it's worth reconsidering your setup and exploring better resource management approaches.

### Resource Management Review

**Architecture Assessment:** When Elastic IP requirements multiply, this typically indicates an opportunity to redesign your architecture using more cloud-native approaches like auto-scaling groups, load balancers, and DNS-based routing.

### Best Practice Summary

Use Elastic IPs sparingly and only when specific technical requirements demand static IP addresses. For most modern applications, DNS-based routing and load balancing provide superior solutions that align better with cloud scalability principles.

## Security Groups and Networking Key Takeaways

### Security Group Fundamentals

- **Virtual firewalls** that control traffic flow to and from EC2 instances
- **Allow rules only** with default deny for anything not explicitly permitted
- **Stateful operation** where allowed inbound traffic automatically permits corresponding outbound responses
- **Port and IP-based control** with support for referencing other security groups


### Network Traffic Control

- **Inbound traffic blocked by default** requiring explicit rules for access
- **Outbound traffic allowed by default** enabling internet connectivity
- **Immediate rule effects** with changes taking place instantly
- **Layer above instances** filtering traffic before it reaches servers


### IP Address Management

- **IPv4 remains dominant** for most current applications
- **Private IP addresses** for internal network communication with reusability across networks
- **Public IP addresses** for internet-facing services with global uniqueness requirements
- **Dynamic public IPs** assigned automatically with option for static Elastic IPs


### Elastic IP Considerations

- **Static public addressing** available when consistent IP addresses are required
- **Cost implications** for unused addresses encouraging proper resource management
- **Limited allocation** with five per account by default
- **Modern alternatives** like DNS and load balancers often provide better architectural solutions


### Troubleshooting Guidelines

- **Timeout issues** typically indicate security group blocking
- **Connection refused errors** usually point to application problems
- **Security group separation** recommended for different access types (SSH, web traffic)
- **Rule specificity** maintains security while enabling necessary functionality


### Best Practices

- **Principle of least privilege** by opening only necessary ports to trusted sources
- **Group-based management** for easier administration across multiple instances
- **DNS-based routing** preferred over static IP dependency
- **Regular rule review** to maintain appropriate access controls

These concepts form the foundation of AWS network security, providing the tools needed to build secure, scalable applications while maintaining proper access control and traffic management.


