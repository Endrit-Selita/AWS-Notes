# AWS Load Balancing & Scalability – Comprehensive DevOps Notes

---

# Lesson 56. Scalability & High Availability

### Understanding Core Cloud Computing Concepts

Two fundamental concepts in cloud computing are **scalability** and **high availability (HA)**. While related, they serve different purposes in building robust systems.

### What is Scalability?

**Scalability** means your application or system can handle increasing loads by adapting to demand. As traffic or workloads grow, your system scales to meet that demand effectively.

### Types of Scalability

### Vertical Scalability (Scaling Up)

**Adding More Power:** This involves adding more power to your existing system, similar to upgrading your computer by adding more CPU, RAM, or storage. The machine becomes more powerful, but it remains the same single machine.

### Horizontal Scalability (Elasticity)

**Adding More Instances:** This means adding more instances of a resource to handle the load. Instead of making one server bigger, you add more servers to distribute the workload.

**Elasticity Concept:** Horizontal scalability is often referred to as elasticity because it allows you to scale in and out based on demand, like elastic that stretches and contracts.

### High Availability (HA)

**System Resilience:** High availability ensures your system stays up and running even when parts of it fail. While scalability handles greater loads, high availability focuses on maintaining uptime during failures.

### Key Distinction

**Different Purposes:** You can have a highly available system that doesn't scale well. Scalability and high availability address different challenges and work together to create robust applications.

**Call Centre Analogy:**

- **Vertical scaling:** Hiring one person but giving them better equipment, faster computer, and more resources to handle more calls
- **Horizontal scaling:** Hiring more people to answer calls so no single person becomes overwhelmed
- **High availability:** Having backup staff available on standby to ensure the call centre runs smoothly even if someone becomes unavailable


---


# Lesson 57. Vertical Scalability

### Understanding Vertical Scaling

**Vertical scalability** means increasing the size of the instance or resource you're using. You're essentially adding more power to the same server rather than adding more servers.

### Practical Example

If your application runs on a t2.micro instance, scaling vertically means upgrading to a more powerful instance like t2.large. This provides the same server but with more CPU, RAM, and storage capacity.

### When to Use Vertical Scaling

### Non-Distributed Systems

**Database Applications:** Vertical scaling is common for non-distributed systems such as databases. Services like RDS or ElastiCache can improve performance when more resources are needed by upgrading the instance size to handle larger workloads or more complex queries.

### The Scaling Limit

**Hardware Constraints:** There's always a limit to how much you can vertically scale, determined by available hardware. Once you reach the largest available instance type, you cannot continue scaling up and must explore horizontal scaling options.

**Instance Size Progression:** You can scale from small instances to massive ones (like u-12tb1.metal with 12.3TB RAM and 448 vCPUs), but eventually hit hardware limits.

### Company Promotion Analogy

Think of vertical scaling like promoting someone in your company. You start with a junior operator (t2.micro) and as responsibilities grow, promote them to senior operator (t2.large), giving them better tools to handle tasks. However, one person can only handle so much, and eventually you need to hire more people to spread the workload.

### Strategic Considerations

**First Step Approach:** Vertical scaling is often the first step when you need to improve performance or handle larger loads, but it's important to understand the limitations.

**Transition Planning:** For applications that need to grow beyond single-machine limits, horizontal scalability will eventually become necessary.

---


# Lesson 58. Horizontal Scalability

### The Distributed Systems Approach

**Horizontal scalability** means increasing the number of instances or systems to handle more load. Instead of upgrading one machine like in vertical scaling, you add more machines or instances to distribute the workload.

### Core Distributed Systems Concept

**Workload Distribution:** This is the fundamental idea behind distributed systems. Instead of relying on one powerful machine, you spread the workload across multiple smaller ones, with each machine handling part of the work.

**Increased Capacity:** This approach allows you to handle much larger amounts of data and traffic than any single machine could manage.

### Benefits for Modern Applications

### Resilience and Reliability

**Failure Tolerance:** Horizontal scaling is particularly valuable for web applications and modern cloud-based systems because if one instance fails, others can take over, adding resilience to the system.

**Easy Management:** It's easier to manage in the long run because the system continues operating even when individual components fail.

### Elasticity in Action

**Traffic Spike Management:** Consider a website that suddenly experiences a huge traffic spike. With horizontal scaling, you can easily spin up more instances to handle the extra traffic, then scale back down when traffic reduces.

**Flexible Response:** This flexibility is why horizontal scaling is often called "elastic scaling" because it adapts dynamically to changing conditions.

### AWS Implementation

**Cloud Services Integration:** Horizontal scaling is easy to implement with cloud services like EC2, and AWS makes it simple to spin up new instances when needed.

**Automation Capabilities:** You can automate the entire process with Auto Scaling Groups, eliminating manual intervention.

### Call Centre Analogy Applied

If you have one person answering phones (vertical scaling), there's only so much they can handle. But if you bring in more people (horizontal scaling), each person handles a portion of the calls, and your capacity grows exponentially. The more people you add, the more calls you can handle.

### System Architecture Benefits

**Unpredictable Workloads:** Horizontal scaling is essential for systems that need to handle unpredictable or fluctuating workloads.

**Growth and Resilience:** It's not only about growth but also about resilience. If one instance fails, the others keep the system running smoothly.

---


# Lesson 59. High Availability

### What is High Availability?

**High Availability (HA)** refers to running your application or system in multiple locations to ensure that if one part of your infrastructure fails, another part can take over seamlessly.

### Relationship with Horizontal Scaling

**Complementary Concepts:** HA usually goes hand in hand with horizontal scaling because to be highly available, you need multiple instances or systems across different locations.

### AWS Implementation Strategy

**Multi-AZ Architecture:** In AWS, we typically achieve high availability by running applications across at least two Availability Zones (AZs). AZs function like independent data centres, often located in different geographical regions.

**Data Centre Loss Protection:** The goal of HA is to survive a data centre loss. If one data centre or AZ goes down due to an outage, your application should continue running in another zone without downtime.

### Types of High Availability

### Passive HA

**Standby Systems:** In some cases, HA can be passive. For example, with RDS Multi-AZ, your primary database runs in one AZ while a backup secondary database is maintained in another. If the primary fails, AWS automatically switches to the secondary without manual intervention.

### Active HA

**Distributed Workloads:** When using horizontal scaling, HA can be active. You distribute workloads across multiple instances and AZs. If one instance or AZ fails, traffic is automatically routed to remaining healthy instances, ensuring continuous availability.

### Real-World Implementation

**Multiple Location Strategy:** Think of running a call centre with two buildings in different cities. If something happens to the first building (power failure, network issues, or other problems), the team in the second building can continue answering calls, ensuring service continuity regardless of location-specific issues.

### Business Continuity Benefits

**Seamless User Experience:** This setup ensures your application remains available to users even during outages, maintaining business operations and user satisfaction.

**Automatic Failover:** Modern HA implementations provide automatic failover, reducing the need for manual intervention during failure scenarios.

---


# Lesson 60. High Availability \& Scalability for EC2

### Bringing Concepts Together

Let's examine how high availability and scalability apply specifically to EC2 instances, combining all the concepts we've covered.

### Vertical Scaling with EC2

**Instance Size Progression:** With vertical scaling, you increase the size of your EC2 instance to make it more powerful by adding more RAM, CPU, or storage.

**Scaling Range:** You might start with t2.nano (0.5 GB RAM, 1 vCPU) and scale up to massive instances like u-12tb1.metal (12.3 TB RAM, 448 vCPUs).

**Hardware Limitations:** Remember, there's always a limit to how large you can scale. Once you hit the hardware limit, you need to consider horizontal scaling.

### Horizontal Scaling Implementation

**Adding More Instances:** With horizontal scaling, you add more instances to handle load instead of making one server bigger.

**Auto Scaling Groups:** In AWS, this is typically implemented using Auto Scaling Groups (ASG), which automatically add or remove EC2 instances based on demand.

**Dynamic Response:** For example, if your website traffic spikes, ASG launches more instances to handle the load and scales them back down when traffic decreases.

### Load Balancer Integration

**Traffic Distribution:** Load balancers are often used with horizontal scaling to distribute incoming traffic across all available instances, ensuring no single instance becomes overloaded.

**Even Distribution:** This ensures optimal resource utilisation and performance across your infrastructure.

### High Availability with EC2

**Multi-AZ Distribution:** HA involves running instances across multiple Availability Zones, ensuring that if one AZ goes down, your application remains available in another AZ.

**Auto Scaling Group Distribution:** You can configure Auto Scaling Groups with multiple AZs to ensure instances are distributed across different zones, adding resilience to your application.

**Load Balancer HA:** Load balancers also support multi-AZ configuration, distributing traffic across instances in multiple AZs. If an instance or entire AZ becomes unavailable, traffic automatically redirects to instances in another AZ.

### Complete Implementation Example

**Comprehensive Strategy:** Imagine running an application where you want both scalability and high availability:

1. **Start Small:** Begin with a single instance and grow vertically if needed
2. **Scale Horizontally:** Add more instances using horizontal scaling as traffic increases
3. **Implement ASG:** Use Auto Scaling Groups for automatic scaling
4. **Distribute Geographically:** Distribute instances across multiple AZs with a load balancer
5. **Ensure Continuity:** Keep your application running smoothly even if parts fail

### Foundation of Cloud Infrastructure

**Flexibility and Resilience:** The combination of vertical scaling, horizontal scaling, and high availability is what makes cloud infrastructure so flexible and resilient, enabling applications to handle varying loads while maintaining high uptime.

---


# Lesson 61. What is Load Balancing?

### Understanding Load Balancing

**Load balancing** is a method to distribute traffic across multiple servers or EC2 instances. Instead of sending all user traffic to one instance, a load balancer acts as a traffic coordinator, distributing requests across different servers.

### Restaurant Kitchen Analogy

Picture a busy restaurant with only one chef where all customers place orders simultaneously. The chef becomes overwhelmed. However, with a team of chefs (multiple EC2 instances) and a manager (load balancer) directing each order to the next available chef, everything runs smoothly. Customers get served faster and the kitchen doesn't become overloaded.

### How Load Balancing Works

**Traffic Distribution:** The Elastic Load Balancer (ELB) in AWS sits between your users and your EC2 instances. When traffic arrives, it forwards requests to the EC2 instances downstream.

**Health Monitoring:** The load balancer continuously checks which instances are healthy and directs traffic only to instances that can handle requests properly.

**Automatic Management:** This process keeps your application available and responsive even if one or more instances fail. The load balancer automatically redirects traffic to healthy instances without requiring manual intervention.

### Reverse Proxy Functionality

**Enhanced Features:** A reverse proxy is similar to a load balancer but offers additional functionality. It sits between users and servers, handling requests, but can do more than just distribute traffic.

**AWS Implementation:** In AWS, services like Application Load Balancer (ALB) provide reverse proxy features, including:

- Routing traffic based on request content
- Directing traffic to different services or microservices
- Content-based routing decisions


### Practical Example

**Three-Instance Setup:** Imagine you have an application with three EC2 instances running. The ELB sits in front of them, and when users connect, the load balancer spreads traffic across all three instances.

**Failure Handling:** If one instance goes down, the load balancer automatically stops sending traffic to the failed instance and directs it to the remaining healthy instances, ensuring seamless user experience.

### Building Scalable Applications

**Key Infrastructure Components:** Load balancing and reverse proxies are fundamental to building scalable and resilient applications. They ensure users receive the best experience even as traffic grows or instances fail.

---


# Lesson 62. Why Use a Load Balancer?

### Primary Benefits of Load Balancing

### Spread the Load

**Traffic Distribution:** The primary job of a load balancer is to distribute incoming traffic across multiple downstream instances. This prevents any single instance from becoming overloaded and ensures a smoother experience for users.

### Single Point of Access

**Simplified DNS Management:** With a load balancer, users don't need to know the addresses of individual instances. They simply connect to the load balancer's DNS endpoint, which handles directing traffic to the appropriate destination behind the scenes.

### Handle Instance Failures

**Automatic Failover:** If any instance fails or becomes unhealthy, the load balancer automatically stops sending traffic to it and redirects traffic to other healthy instances. Users might not even notice that something went wrong, as the service continues operating normally.

### Regular Health Checks

**Continuous Monitoring:** Load balancers constantly check the health of your instances. When one goes down, the load balancer detects this and redirects traffic accordingly, keeping your application running smoothly even during failure scenarios.

### Advanced Features

### SSL Termination (HTTPS)

**Certificate Management:** You can configure load balancers to handle SSL certificates and HTTPS traffic for websites. The load balancer manages the heavy lifting of encrypting and decrypting traffic, freeing up your EC2 instances to focus on application logic.

### Sticky Sessions (Session Persistence)

**User Consistency:** Sometimes you want a user's session to remain on the same server. Sticky sessions ensure that when needed, users are sent back to the same instance for their requests using cookies.

### High Availability Across Zones

**Multi-AZ Support:** Load balancers are designed for high availability by spreading traffic across multiple Availability Zones. They ensure your application remains online even if one zone experiences issues.

### Traffic Separation

**Public and Private Traffic:** In more complex architectures, you might want to separate public traffic (user-facing) from private traffic (internal). Load balancers can help route traffic appropriately to ensure security and proper flow.

### Comprehensive Infrastructure Benefits

**Essential for Modern Applications:** Using a load balancer is essential for building resilient, scalable, and secure applications. It provides much more than traffic distribution, including failover handling, security improvements, and high availability assurance.

---


# Lesson 63. Why Use an Elastic Load Balancer?

### Managed Load Balancer Benefits

**ELB (Elastic Load Balancer)** is a managed load balancer service, meaning AWS handles most of the complexity for you.

### Key Advantages

### AWS Reliability Guarantee

**Built and Maintained by AWS:** ELB is constructed and maintained by AWS, so you can trust it will keep running without worrying about underlying infrastructure management.

**Automated Maintenance:** AWS handles upgrades and maintenance automatically. Unlike self-managed load balancers (like Nginx or HAProxy) where you need to handle updates and potential downtime, AWS manages everything behind the scenes, including ensuring high availability.

### Simplified Configuration

**Reduced Complexity:** ELB comes with streamlined configuration options. AWS provides the essential settings while you focus on defining rules and routing logic. They handle the technical infrastructure details.

### DIY vs Managed Comparison

### Self-Managed Options

**Cost Considerations:** You can set up your own load balancer using tools like Nginx or HAProxy, which might cost less upfront.

**Operational Overhead:** However, this approach requires significantly more work. You need to handle maintenance, monitoring, scaling, and fault tolerance independently.

### Managed Service Benefits

**Focus on Applications:** With ELB, AWS manages all infrastructure complexity, allowing you to focus on your application development rather than infrastructure management.

### Deep AWS Integration

**Seamless Service Connection:** ELB is fully integrated with many other AWS services, making it a powerful option for comprehensive cloud architectures.

### Integration Examples

### EC2 and Auto Scaling Groups

**Automatic Scaling:** ELB works perfectly with EC2 instances and Auto Scaling Groups. It automatically distributes traffic to new instances as they're added, ensuring seamless scaling operations.

### AWS Certificate Manager (ACM)

**SSL Management:** ACM handles SSL certificates, and ALB can terminate SSL connections, simplifying your security setup significantly.

### CloudWatch Integration

**Performance Monitoring:** ELB integrates with CloudWatch, enabling you to monitor performance and health metrics for your load balancers.

### Additional Service Integration

**Ecosystem Benefits:** ELB works with Route 53 for DNS routing, WAF for security, and Global Accelerator for performance improvements across regions, creating a comprehensive AWS ecosystem.

### Value Proposition

**Cost vs Benefit Analysis:** While ELB might cost more than self-managed solutions, it saves significant time and effort in the long run. AWS handles the complex work of ensuring constant availability, allowing you to focus on core business logic rather than infrastructure management.

---


# Lesson 64. Health Checks

### Understanding Health Checks

**Health checks** enable a load balancer to determine if the instances it's forwarding traffic to are healthy and able to respond properly. Without health checks, the load balancer might continue sending traffic to instances that are down or not functioning correctly, causing service problems.

### How Health Checks Work

**Request-Based Monitoring:** The load balancer checks instance health by sending requests to a specific port and route. A common example is the `/health` endpoint, which can be configured to report on instance status.

### Practical Implementation

**Example Configuration:**

- **Protocol:** HTTP
- **Port:** 4567
- **Route:** `/health`
- **Expected Response:** 200 OK status

**Health Determination:** If the instance returns a 200 OK status, it's considered healthy, and the load balancer continues sending traffic to it.

### Unhealthy Instance Handling

**Problem Detection:** If the response isn't 200 OK, this indicates an issue with the instance. It might be down, unresponsive, or experiencing problems.

**Traffic Redirection:** The load balancer marks the instance as unhealthy and stops sending traffic to it, protecting users from failed requests.

### Why Health Checks are Crucial

### Automated Management

**Continuous Monitoring:** Health checks are automated and keep your application running smoothly. The load balancer continuously monitors your instances without manual intervention, ensuring users are only sent to instances that can handle requests properly.

### Automatic Recovery

**Self-Healing Systems:** If an instance fails, the load balancer automatically routes traffic to other healthy instances until the failed instance comes back online and passes health checks again.

### User Experience Protection

**Seamless Service:** This automation is vital for user experience. Users expect functional, responsive applications without encountering failed requests or service interruptions.

### Real-World Example

**Multi-Instance Scenario:** Imagine running multiple EC2 instances behind a load balancer. One instance stops responding due to high CPU usage or application errors.

**Automated Response:** The health check detects this issue and marks the instance as unhealthy. The load balancer then automatically reroutes traffic to remaining healthy instances, preventing any service disruption for users.

**Transparent Recovery:** Users continue receiving service while the problematic instance is either repaired or replaced, creating a transparent, resilient system.

---


# Lesson 65. Types of Load Balancers on AWS

### AWS Load Balancer Family

AWS offers several types of load balancers, each designed for specific use cases and technological requirements.

### Classic Load Balancer (CLB)

**Legacy Option:** The oldest generation of load balancers, introduced by AWS in 2009. While still available, it's not commonly used for new implementations.

**Basic Functionality:** CLB supports basic HTTP, HTTPS, TCP, and SSL traffic. It's simple and gets the job done but lacks the advanced features of newer load balancers.

**Limitation:** AWS recommends using newer generation load balancers for new projects due to enhanced capabilities and features.

### Application Load Balancer (ALB)

**Modern Web Applications:** Released in 2016, ALB is part of the new generation of load balancers designed specifically for HTTP, HTTPS, and WebSocket traffic, making it ideal for modern web applications.

**Layer 7 Intelligence:** ALB operates at Layer 7 (application layer), meaning it's intelligent and can make routing decisions based on request content, including URLs, headers, and cookies.

**Microservices Support:** This makes it perfect for microservices or container environments where different services need different routing logic.

### Network Load Balancer (NLB)

**High Performance:** Released in 2017, NLB is a Layer 4 load balancer operating at the transport layer, designed for TCP and UDP traffic.

**Ultra-Low Latency:** Built for high-performance scenarios requiring very low latency, NLB is ideal for handling millions of requests per second.

**Specialised Use Cases:** Perfect for high-throughput, low-latency applications such as real-time gaming or high-frequency trading systems.

### Gateway Load Balancer (GLB)

**Network Applications:** A newer addition that operates at Layer 3 (network layer) and works with IP protocol.

**Third-Party Integration:** Designed to help deploy, scale, and manage third-party network applications like firewalls, intrusion detection systems, and traffic analysers.

**Complex Networking:** Useful for more sophisticated networking setups requiring advanced security or analysis capabilities.

### Choosing the Right Load Balancer

### Recommendation Strategy

**Avoid Legacy:** While CLB still functions, AWS recommends using new generation load balancers (ALB, NLB, GLB) due to enhanced features, capabilities, and ongoing support.

### Deployment Options

**Internal vs External:** Load balancers can be configured as either internal (private) or external (public) depending on traffic routing requirements.

**Example Configurations:**

- **Internal ALB:** Route traffic within your VPC
- **External ALB:** Handle traffic from the public internet


### Use Case Guidelines

### Traditional Web Applications

**Choose ALB:** For standard web applications, use ALB to take advantage of content-based routing and modern protocols like WebSockets.

### High-Performance Requirements

**Choose NLB:** Unless your application requires handling large volumes of TCP traffic with minimal latency, NLB is the appropriate choice.

### Advanced Networking

**Choose GLB:** For network applications like firewalls, security setups, and advanced networking configurations, Gateway Load Balancer is the optimal solution.

---


# Lesson 66. Load Balancer Security Groups

### Security Group Configuration Strategy

When working with load balancers and EC2 instances, proper security group configuration is essential to ensure traffic flows safely while maintaining security.

### Load Balancer Security Group

**Internet-Facing Access:** The security group for the load balancer itself should allow users to access the load balancer from anywhere on the internet to reach your website or application.

**HTTP Traffic (Port 80):** Allow unencrypted HTTP traffic to reach the load balancer for basic web access.

**HTTPS Traffic (Port 443):** Allow encrypted HTTPS traffic using SSL/TLS to the load balancer for secure communications.

**Source Configuration:** The source for these rules is set to `0.0.0.0/0`, meaning the load balancer can accept traffic from any IP address on the internet.

### Application Security Group

**Restricted Backend Access:** This applies to EC2 instances behind the load balancer. The goal is to restrict access so only the load balancer can communicate directly with EC2 instances.

**Load Balancer Source Rule:** Configure rules to allow HTTP (port 80) traffic specifically from the load balancer security group, not from the entire internet.

**Protection Layer:** This setup ensures your EC2 instances are protected from direct internet access. The only traffic they accept comes from the load balancer, which acts as a protective barrier.

### Security Architecture Benefits

### Controlled Access Pattern

**Single Entry Point:** Users can only communicate with the load balancer, which then forwards legitimate traffic to your EC2 instances.

**Instance Protection:** Backend servers are shielded from direct access from the internet, reducing attack surface and security risks.

### Building Security Analogy

Think of the load balancer as the front door to a building. Users (customers) come through this controlled entrance, but they don't get direct access to everything inside. The load balancer decides which rooms (EC2 instances) they can enter, and each room maintains its own restricted access controls.

### Common Architecture Pattern

**Industry Standard:** This security group setup is extremely common in cloud architecture because it ensures secure traffic flow while maintaining control and protection for backend infrastructure.

**Scalable Security:** This approach not only ensures secure traffic flow but also helps maintain control and protection as your system scales, keeping EC2 instances protected from direct external access while enabling legitimate traffic through the load balancer.

---


# Lesson 67. Application Load Balancer

### ALB Core Characteristics

**Application Load Balancers (ALB)** are game-changers for modern application architectures due to their intelligent traffic handling capabilities.

### Layer 7 Operation

**HTTP Layer Intelligence:** ALB operates at Layer 7 (application layer), specifically focusing on HTTP and HTTPS traffic. This means it understands and can analyse the content of requests, including headers, cookies, URL strings, and other application-level information.

### Advanced Routing Capabilities

### Multi-Application Support

**Target Group Distribution:** ALB can load balance traffic to multiple HTTP applications running across different machines, all organised within target groups.

**Same-Machine Applications:** It can also balance traffic to multiple applications running on the same machine, which is particularly useful in container environments where several applications might run on a single EC2 instance or ECS service.

### Protocol Support

**HTTP/2 Integration:** ALB comes with built-in HTTP/2 support. HTTP/2 is a more efficient version of HTTP that allows better performance and can handle more connections simultaneously.

**WebSocket Support:** Essential for real-time communication applications like chat services or live dashboards where updates need to happen instantly.

### Redirect Capabilities

**HTTPS Redirection:** ALB supports automatic redirects, such as redirecting HTTP traffic to HTTPS for enhanced security, ensuring all traffic uses encrypted connections.

### Modern Architecture Benefits

**Container and Microservices:** ALB's intelligent routing makes it perfect for modern architectures including containers and microservices, where different services require different routing logic based on request characteristics.

---


# Lesson 68. Application Load Balancer Advanced Features

### Target Group Routing

**Multiple Destinations:** ALBs can direct traffic to different target groups, which can contain EC2 instances, Lambda functions, or containers. This flexibility makes ALB suitable for handling diverse types of workloads within a single load balancer.

### Advanced Routing Methods

### Path-Based Routing

**URL Path Logic:** Route traffic based on the URL path. For example:

- Requests to `/users` go to one target group
- Requests to `/posts` go to another target group
- Perfect for microservices architecture where each path is handled by a different service


### Host-Based Routing

**Domain-Based Distribution:** Route traffic based on the hostname in the URL:

- `blog.coderco.io` traffic goes to blog services
- `news.coderco.io` traffic goes to news services
- Allows running multiple domains on the same ALB


### Query String and Header-Based Routing

**Granular Control:** ALB can route traffic based on:

- Query strings (e.g., `coderco.io/user?id=456&order=false`)
- HTTP headers (e.g., requests from mobile devices versus desktop)
- Provides extensive control for personalised or device-specific experiences


### Container Integration

### Microservices and Container Support

**Docker and ECS Integration:** ALB is naturally suited for microservices and container-based applications running on Docker or Amazon ECS.

**Multi-Service Management:** In container environments where multiple services run on the same machine, ALB can distribute traffic to each service based on specific ports or paths.

### Port Mapping for ECS

**Dynamic Port Management:** When running ECS, ALB features port mapping capability, allowing it to dynamically direct traffic to containers running on different ports.

**Automatic Discovery:** This ensures that even as containers are deployed and scaled across various ports, ALB knows where to send traffic automatically.

### Cost and Management Efficiency

### Single Load Balancer Strategy

**Multiple Applications:** Unlike Classic Load Balancers that require separate load balancers for each application, ALB can manage multiple applications with a single load balancer thanks to its advanced routing features.

**Significant Improvement:** This represents a massive improvement in terms of cost and infrastructure management complexity.

### Microservices Example

**Three-Service Architecture:** Imagine you have three microservices:

1. **User Service:** Handles user management
2. **Posts Service:** Manages content posts
3. **Comments Service:** Handles user comments

**Single ALB Solution:** With ALB, you can use path-based routing to send:

- `/users` requests to the user service
- `/posts` requests to the posts service
- `/comments` requests to the comments service

All while using just one load balancer instead of three separate ones.

---


# Lesson 69. Application Load Balancer HTTP Traffic Flow

### Traffic Flow Architecture

Let's examine how ALBs handle HTTP-based traffic in a typical web application scenario.

### External ALB Configuration

**Front-End Position:** An external ALB sits in front of your application, acting as the primary entry point for all user requests.

**User Request Handling:** Users send HTTP requests to the ALB, which then routes those requests to appropriate target groups based on configured routing rules.

### Target Group Organisation

**Backend Resources:** Target groups consist of EC2 instances or other resources like ECS tasks or Lambda functions responsible for processing requests.

**Service-Specific Grouping:** Target groups are usually organised around specific services:

- One target group handles user-related tasks (login, profile management)
- Another target group handles product searches and catalogue management
- Additional target groups for other business functions


### Health Check Integration

**Continuous Monitoring:** As part of its operation, ALB uses health checks to ensure instances in each target group are running and able to handle traffic effectively.

**Automatic Traffic Management:** If a health check fails (meaning an instance is unresponsive or experiencing problems), ALB stops sending traffic to that instance and routes requests to other healthy instances in the group.

### HTTP/HTTPS Traffic Handling

**Web Service Focus:** ALB is specifically built for HTTP and HTTPS traffic, making it capable of handling a wide range of web-based services and applications.

**Request Analysis:** Each incoming request is examined by ALB, which determines where to send the traffic based on path, host, or other routing rules you've configured.

### Microservices Benefits

**Service Separation:** The ability to separate traffic into different target groups makes ALB ideal for microservices applications with multiple distinct services.

**Single Load Balancer Management:** You can route requests to different parts of your application while using just one load balancer, simplifying management and reducing costs.

### Practical Example

**Website with Multiple Services:**

- **User Profile Service:** When a user requests to update their profile, ALB examines the path (`/users`) and routes traffic to the target group handling user-related functionality
- **Search Service:** A search request gets routed to a separate target group focused on search-related functionality

**Service Isolation:** By using different target groups, you ensure one service doesn't interfere with another, allowing your application to scale and perform better with clear separation of concerns.

---


# Lesson 70. Application Load Balancer Target Groups

### Understanding Target Groups

**Target groups** are collections of resources like EC2 instances, Lambda functions, or ECS tasks that your ALB routes traffic to. Think of them as organised destinations for incoming requests that the load balancer manages.

**Service Organisation:** Each target group is typically tied to a specific service or application, allowing you to scale different parts of your system independently.

### Types of Target Group Resources

### EC2 Instances

**Auto Scaling Integration:** EC2 instances can be managed by Auto Scaling Groups to automatically add or remove instances based on load. ALB routes HTTP traffic to these instances, ensuring requests are balanced between them.

### ECS Tasks

**Container Applications:** When using ECS, ALB can route traffic to ECS tasks, which are essentially containers running your applications. This is ideal for microservices and containerised applications.

### Lambda Functions

**Serverless Integration:** ALB supports routing HTTP requests to Lambda functions. The load balancer translates requests into JSON events that Lambda functions can process, making it excellent for serverless applications where you don't want to manage infrastructure.

### Private IP Addresses

**Direct IP Routing:** If you're routing traffic to IP addresses directly instead of instances or functions, those IPs must be private IP addresses within your VPC.

### Multiple Target Group Management

### Single ALB, Multiple Services

**Efficient Resource Usage:** ALBs allow you to route traffic to multiple target groups, meaning you can handle several services or applications with a single ALB.

**Service Examples:**

- One target group for handling user requests
- Another target group for search services
- Additional target groups for different business functions


### Health Check Implementation

**Target Group Level Monitoring:** Health checks are performed at the target group level. ALB routinely checks the health of each resource in target groups, whether they're instances, ECS tasks, Lambda functions, or other resources.

**Automatic Traffic Management:** If a resource becomes unhealthy, ALB stops routing traffic to it until it returns to a healthy state, ensuring users are always directed to functioning resources.

### Scaling and Management Benefits

**Independent Scaling:** Each target group can scale independently based on its specific load and requirements, providing granular control over your application's capacity management.

**Service Isolation:** Different services can have different scaling patterns, health check requirements, and resource specifications while being managed through a single load balancer.

---


# Lesson 71. Application Load Balancer Good to Know

### Fixed Hostname Configuration

**Automatic DNS Management:** ALB provides each load balancer with a fixed hostname in the format `XXX.region.elb.amazonaws.com`. This URL is what your clients use to access services through the load balancer.

**AWS Management:** Unlike some load balancers where you manage domain names yourself, AWS automatically provides and maintains this hostname for you.

**Custom Domain Integration:** If you need something more customised, you can set up a custom domain name using Route 53 and point it to this AWS-provided hostname.

### Client IP Address Handling

### Connection Termination

**IP Address Challenge:** Your application servers won't see the client's IP address directly. When a client connects to ALB, the connection terminates at the load balancer, meaning requests appear to come from the ALB's private IP rather than the client's actual IP.

### X-Forwarded Headers Solution

**Client IP Recovery:** AWS provides a way to pass along the client's actual IP address using special HTTP headers:

**X-Forwarded-For Header:** Contains the true client IP address. Your application must read this header if you need the real client's IP address.

**Additional Headers:**

- **X-Forwarded-Port:** Contains the port the client used to connect
- **X-Forwarded-Proto:** Contains the protocol (HTTP/HTTPS) the client used


### Practical Implementation Example

**Client Connection Scenario:** A client with IP address `12.34.56.78` connects to your load balancer to access your application.

**What Your EC2 Instance Sees:** Instead of seeing the client's actual IP address, your EC2 instance sees the load balancer's private IP address.

**Retrieving Real Client IP:** To get the real client's IP, your application needs to examine the `X-Forwarded-For` header where the original IP address is stored.

### Use Cases for Client IP Information

**Important Scenarios:**

- **Geo-location:** Determining user location for content personalisation
- **Rate limiting:** Implementing per-IP rate limits for security
- **Security auditing:** Logging access patterns and potential security threats
- **Analytics:** Understanding user geographic distribution


### Application Configuration Requirements

**Header Processing:** Ensure your application is configured to read `X-Forwarded-For` headers if client IP information is necessary for your application's functionality, logging, or security requirements.

**Development Considerations:** This is particularly important when migrating applications from direct server access to load balancer configurations, as the IP handling behaviour changes.

---


# Lesson 72. Network Load Balancer

### High-Performance Load Balancing

**Network Load Balancers (NLB)** are optimised for handling extreme performance requirements and high traffic volumes with ultra-low latency.

### Layer 4 Operation

**Transport Layer Focus:** NLB operates at Layer 4 of the OSI model, which means it handles TCP and UDP traffic at the transport layer rather than examining application-level content.

**Performance Optimisation:** It's specifically designed for high-performance use cases where you need to manage millions of requests per second efficiently.

### Key Performance Benefits

### Ultra-Low Latency

**Speed Comparison:** NLB provides approximately 100 milliseconds latency compared to ALB's 400 milliseconds, making it ideal when lightning-fast response times are critical.

### High Throughput

**Massive Scale Handling:** Capable of handling millions of requests per second, making it perfect for applications with high throughput requirements or those that rely heavily on performance.

**Ideal Use Cases:** Financial services, gaming applications, real-time communication systems, or any application where milliseconds matter.

### Static IP Configuration

### Predictable Endpoints

**One Static IP per AZ:** NLB assigns one static IP address per Availability Zone, which is a significant advantage when you need predictable, static endpoints for client connections.

**Security Integration:** This is particularly useful for security configurations like IP whitelisting, where clients need to know specific IP addresses to connect to.

### Elastic IP Support

**Custom IP Assignment:** You can assign Elastic IPs to your NLB if needed, making it easier to maintain the same IP addresses even when you change or update your infrastructure.

**Permanent Connections:** This is helpful when dealing with services or clients that need to connect permanently to specific IP addresses.

### Protocol Specialisation

**TCP and UDP Traffic:** NLB is particularly well-suited for TCP and UDP traffic rather than HTTP/HTTPS.

**Specialised Applications:** If your application relies on extreme performance, real-time processing, or protocols like DNS, gaming services, or VoIP, NLB is the appropriate choice over ALB.

### Cost Considerations

**Not Free Tier:** Important to note that NLB is not included in the AWS free tier, so be prepared for costs when deploying in production environments.

### Real-World Example

**Financial Trading Platform:** Imagine a company running a real-time trading platform where every millisecond counts for trade execution. Using NLB makes sense because it minimises latency and can handle massive amounts of traffic very quickly, ensuring users get fast data and the company can maintain stability under heavy loads.

**Performance Critical Applications:** Any application where raw speed and throughput are more important than intelligent content routing will benefit from NLB's specialised performance characteristics.

---


# Lesson 73. Network Load Balancer TCP Traffic

### Understanding TCP Layer 4 Traffic

**Transport Layer Operation:** As discussed in the networking module, Layer 4 is the transport layer where the TCP protocol operates. NLB's job is to handle traffic at this level, routing raw TCP or UDP traffic to your instances without involving higher-level protocols from Layer 7 like HTTP or HTTPS.

### Traffic Routing Mechanism

**Rule-Based Distribution:** In the traffic flow diagram, NLB routes TCP traffic based on rules you've defined, such as specific ports or protocols, directing this traffic to different target groups handling different types of applications.

### Service-Specific Routing Examples

### User Application Traffic

**TCP Rule Implementation:** If a request comes in for a user application, NLB might use TCP rules to direct traffic to a specific target group running on EC2 instances optimised for handling user data.

### Search Application Traffic

**Mixed Protocol Handling:** Another request for search functionality might come in and be routed based on HTTP traffic. Even though NLB works at the TCP level, HTTP can be handled as a protocol within the TCP transport layer.

### Key NLB Limitations

**No HTTP Inspection:** It's important to understand that NLB doesn't inspect HTTP headers or handle SSL termination, which differs from ALB (Application Load Balancer) functionality.

**Pure Traffic Forwarding:** NLB focuses on efficiently forwarding traffic without modifying it, making it faster and more reliable for raw network performance.

### Optimal Use Cases

### Real-Time Applications

**Performance-Critical Services:** NLB excels in scenarios requiring raw network performance, such as:

- Gaming servers
- Streaming services
- Real-time communication applications
- Any traffic heavily dependent on latency and connection speed


### Multi-Protocol Applications

**Service Differentiation:** This setup is particularly useful when you need to handle different applications that depend on different protocols:

- User applications might need pure TCP traffic handling
- Search applications might work with HTTP within the TCP layer


### When to Choose NLB vs ALB

### NLB Selection Criteria

**Raw Performance Needs:** If you need to handle SSL termination from HTTPS or Layer 7 traffic inspection, ALB would be better suited.

**Speed Priority:** However, if you need raw performance and low-latency TCP or UDP traffic handling, NLB is the ideal choice.

### Performance and Scalability Benefits

**Efficiency Focus:** NLB focuses on speed and efficiency at Layer 4, making it perfect for handling millions of requests with minimal latency.

**Direct Traffic Forwarding:** By forwarding TCP traffic directly without modification, it enables you to handle large amounts of data quickly, making it ideal for applications with high-performance demands and scalability requirements.

---


# Lesson 74. Sticky Sessions (Session Affinity)

### Understanding Sticky Sessions

**Session Affinity Concept:** While a load balancer's primary job is to spread traffic across multiple EC2 instances or targets, sometimes you want users or clients to consistently connect to the same instance, especially when users have ongoing session data.

**Definition:** Sticky sessions ensure that clients are always routed to the same instance behind the load balancer, essentially "sticking" a client to a specific server.

### How Sticky Sessions Work

### Cookie-Based Implementation

**Universal Support:** Sticky sessions work across different load balancer types, whether using CLB (Classic Load Balancer), ALB (Application Load Balancer), or NLB (Network Load Balancer).

**Cookie Mechanism:** Behind the scenes, the load balancer uses cookies to track which instance a client is connected to.

**Configurable Duration:** You can control how long the stickiness lasts by setting an expiration date on the cookie, determining how long a user remains bound to a specific server.

### When to Use Sticky Sessions

### Session Data Storage

**Non-Shared Session Data:** The typical use case is when your application stores session data that isn't shared across instances.

**E-commerce Example:** If a user is interacting with an e-commerce site and their shopping cart data is stored only on one specific instance, you'd want them to stick to that instance so they don't lose their session information.

**Session Continuity:** By keeping users on the same instance, you avoid situations where they might lose their cart contents or session information.

### Trade-offs and Considerations

### Load Distribution Impact

**Potential Imbalances:** When stickiness is enabled, you can potentially overload one instance if too many clients become "stuck" to it, leading to uneven traffic distribution.

**Efficiency Compromise:** Without sticky sessions, traffic spreads more evenly across instances, making resource utilisation more efficient and balanced.

### Performance vs Session Management

**Balance Consideration:** There's a trade-off between maintaining session continuity and achieving optimal load distribution across your infrastructure.

### Practical Implementation Example

### Web Application Login Scenario

**User Session Flow:** Consider a web application where users log in and start sessions on one EC2 instance.

**Stickiness Benefits:** If stickiness is enabled, the load balancer ensures that user stays connected to the same instance for their entire session duration.

**Data Persistence:** This is crucial if session data is stored only on that specific instance, preventing users from losing their login state or application data.

### Configuration Guidelines

### When to Enable Sticky Sessions

**Session-Heavy Applications:** Stickiness is useful for applications with significant session data that isn't shared across multiple instances.

**Use Sparingly:** Only enable sticky sessions when necessary, as they can cause load imbalances in traffic distribution.

### When to Avoid Sticky Sessions

**Load Balance Priority:** If even load distribution and efficiency are more important, and you haven't designed your application to maintain session data in one location, you might want to reconsider enabling stickiness.

### Cookie Management

**Fine-Tuned Control:** You can adjust how long clients stay "stuck" by modifying cookie expiration settings, providing precise control over session affinity duration.

### Decision Framework

**Application Architecture Assessment:** Consider whether your application actually needs sticky sessions. If you're handling critical session data that must stay with one server, stickiness is beneficial. However, if load balance and efficiency are priorities and your application can handle distributed session management, you might want to avoid enabling sticky sessions.

---

# Lesson 75. SSL/TLS Basics

### Understanding SSL/TLS Certificates

**SSL/TLS certificates** are crucial for security on the internet, especially for load balancers that handle traffic between clients and servers.

### What is an SSL Certificate?

**Secure Sockets Layer:** SSL stands for Secure Sockets Layer. SSL certificates ensure that traffic between your clients (like web browsers) and your servers (EC2 instances) is encrypted during transmission.

**In-Flight Encryption:** This is often called "in-flight encryption," meaning data is scrambled as it travels over the internet, preventing anyone from intercepting or reading it.

### SSL vs TLS Evolution

**Modern Security Standards:** You often hear people say "SSL," but what they're really referring to these days is TLS (Transport Layer Security).

**TLS as SSL 2.0:** TLS is the modern, more secure version of SSL. Think of it as SSL 2.0 - same fundamental principles, just better and more secure.

**Common Usage:** Old habits persist, so people still use the term "SSL" to refer to both SSL and TLS certificates. When you see "SSL certificates," know that they're really TLS certificates in modern implementations.

### Certificate Authorities (CAs)

**Trusted Third Parties:** These certificates are issued by Certificate Authorities, which are trusted third-party organisations that verify the identity of websites.

**Common CAs:** Well-known certificate authorities include:

- Comodo
- Symantec
- GoDaddy
- GlobalSign
- DigiCert
- Let's Encrypt (popular free option)


### Certificate Expiration Management

**Time-Limited Validity:** SSL/TLS certificates have expiration dates. When you set them up, you choose a duration: one year, two years, three years, or even up to 10 years for some certificates.

**Renewal Requirements:** After the specified period, certificates need to be renewed to maintain security.

**User Impact:** If a certificate expires, users receive a prominent warning when trying to visit your site, which can damage your application's credibility and user trust.

### Key Security Concepts

### Modern Standards

**TLS Superiority:** TLS is the modern, more secure version of SSL and should be used for new implementations.

### Trust and Authority

**CA Verification:** Certificates are issued by trusted authorities like DigiCert, Let's Encrypt, and many others, ensuring the authenticity of your site.

### Proactive Management

**Renewal Planning:** Set reminders to renew certificates before they expire, or use automated certificate management services that handle renewals automatically.

### Foundation of Web Security

**Essential Security Layer:** SSL/TLS certificates are fundamental to ensuring secure communication over the internet and represent one of the first security layers you should implement when building secure applications or websites.

**Project Integration:** In real-world projects, these certificates are essential for making applications secure from the outset, protecting user data and maintaining trust.

---

# Lesson 76. Load Balancer SSL Certificate Management

### SSL Certificate Integration

**Load balancers act as the middleman** ensuring traffic between users and instances is encrypted using SSL/TLS certificates.

### X.509 Certificate Standard

**Industry Standard Format:** Load balancers use X.509 certificates, which is the technical term for SSL/TLS certificates used in web security.

### AWS Certificate Manager (ACM)

**Simplified Certificate Management:** AWS makes certificate management straightforward through AWS Certificate Manager (ACM), which provides a one-stop solution for creating, renewing, and managing certificates.

**Custom Certificate Option:** If you prefer more control, you can also upload your own custom certificates, though ACM typically provides better integration and automation.

### HTTPS Listener Configuration

When setting up HTTPS listeners on your load balancer, several configuration options are available:

### Default Certificate Requirements

**Primary Certificate:** You must specify a default SSL/TLS certificate that the load balancer uses when no other specific rules are matched.

### Multiple Domain Support

**Multi-Certificate Management:** You can add multiple certificates to handle traffic for different domains, which is especially useful if your load balancer manages traffic for multiple websites or applications.

### Server Name Indication (SNI)

**Intelligent Certificate Selection:** SNI allows clients to specify which hostname they want to connect to, and the load balancer serves the appropriate certificate for that hostname automatically.

### Legacy Support Options

**Backward Compatibility:** You can specify security policies to support older versions of SSL and TLS for legacy clients that haven't updated to modern security standards.

### Traffic Flow Architecture

### HTTPS to HTTP Conversion

**Secure External, Efficient Internal:** Here's how the traffic flow works:

1. **User Connection:** Users connect via HTTPS, encrypting all traffic over the internet
2. **Load Balancer Processing:** The load balancer handles the HTTPS connection and SSL termination
3. **Internal Communication:** Once inside your VPC, the load balancer forwards requests using plain HTTP
4. **Instance Processing:** The request reaches your EC2 instance for processing

### Why This Architecture Works

**Private Network Security:** Since the traffic between the load balancer and EC2 instances travels over private networks within your VPC, encryption isn't necessary for this internal segment.

**Performance Benefits:** This approach reduces the computational overhead on your EC2 instances since they don't need to handle SSL encryption/decryption.

### Security and Compliance Benefits

**Essential for Sensitive Data:** Encryption is critical when handling sensitive data, especially over the internet. Load balancers make this process seamless by integrating certificate management and maintaining security without requiring complex configuration on your part.

**Automated Management:** The integration with ACM means certificates can be automatically renewed, reducing the risk of certificate expiration and service disruption.

---

# Lesson 77. SSL Server Name Indication (SNI)

### The Problem SNI Solves

**Historical Limitation:** Before SNI existed, hosting multiple websites with different SSL certificates on the same server was problematic. You needed a separate IP address for each website with its own certificate, which was inefficient and costly.

### How SNI Works

**Multiple Certificates, Same Server:** SNI fixes this limitation by allowing multiple SSL certificates to be loaded on the same web server, perfect for serving multiple websites from a single server.

### SSL Handshake Process

**Hostname Communication:** When a browser or client makes the initial connection to a web server, it sends the hostname of the website it's trying to reach as part of the SSL handshake process.

**Certificate Selection:** The server uses this hostname information to find and serve the correct SSL certificate for that specific website.

**Fallback Mechanism:** If the server can't find a matching certificate for the requested hostname, it uses the default certificate as a fallback option.

### Practical Benefits

**Multi-Website Hosting:** SNI is extremely helpful if you're running multiple websites on the same server or using modern load balancers that need to handle different domains with their own certificates.

**Cost Efficiency:** This eliminates the old requirement of needing multiple IP addresses for multiple SSL certificates, significantly reducing infrastructure complexity and costs.

### AWS Load Balancer Support

**Modern Load Balancer Compatibility:** SNI works with:

- **ALB (Application Load Balancer):** Full SNI support for multiple certificates
- **NLB (Network Load Balancer):** SNI support for high-performance scenarios
- **CloudFront:** SNI support for content delivery networks


### Legacy Limitations

**Classic Load Balancer:** SNI does not work with CLB (Classic Load Balancer). If you're still using the older Classic Load Balancer, SNI functionality isn't available.

**Upgrade Recommendation:** This is another reason to consider upgrading from Classic Load Balancers to newer generation load balancers.

### Management Simplification

**Modern Certificate Management:** SNI makes SSL certificate management across multiple websites on the same server much easier, eliminating the old requirement of maintaining multiple IP addresses for different certificates.

**Scalable Architecture:** This technology enables more scalable and cost-effective architectures for multi-domain applications and services.

---

# Lesson 78. Elastic Load Balancers SSL Support

### SSL Certificate Support Across Load Balancer Types

Different AWS load balancer types offer varying levels of SSL certificate support and flexibility.

### Classic Load Balancer (CLB)

**Limited SSL Flexibility:** The older generation CLB has significant limitations for SSL certificate management.

**Single Certificate Restriction:** You can only use one SSL certificate per CLB instance.

**Multi-Domain Challenges:** If you want to serve multiple domains with different SSL certificates, you need multiple CLBs, which becomes both cumbersome and costly to manage.

### Application Load Balancer (ALB)

**Enhanced SSL Management:** ALB offers much more flexibility for SSL certificate handling.

**Multiple Certificate Support:** You can attach multiple SSL certificates across multiple listeners, all thanks to SNI (Server Name Indication) support.

**Cost-Effective Multi-Domain:** This means you can serve different domains with different SSL certificates using the same ALB, making it both convenient and cost-efficient.

**Modern Architecture:** This capability is essential for modern applications that need to handle multiple domains or services.

### Network Load Balancer (NLB)

**High-Performance SSL:** Similar to ALB, NLB also supports multiple SSL certificates using SNI technology.

**Performance with Security:** This is particularly valuable for high-performance use cases where you're working with TCP or UDP traffic but still require SSL encryption for security.

**Best of Both Worlds:** NLB provides the performance benefits of Layer 4 load balancing while maintaining the security benefits of SSL/TLS encryption.

### Key Advantages of New Generation Load Balancers

### Flexibility Benefits

**SNI Integration:** The newer generation load balancers (ALB and NLB) provide significantly more flexibility, especially with SSL management, thanks to SNI support.

**Multi-Certificate Management:** You can manage multiple domains and their certificates through a single load balancer, simplifying architecture and reducing costs.

### Upgrade Considerations

**Classic Load Balancer Limitations:** If you're still using Classic Load Balancer, consider upgrading to enjoy the benefits of multiple SSL certificates and more advanced SSL management features.

**Modern Security Requirements:** New generation load balancers better support modern security requirements and certificate management practices.

### Cost and Operational Benefits

**Reduced Infrastructure Complexity:** Using ALB or NLB with multiple certificates eliminates the need for multiple load balancers, reducing both costs and operational complexity.

**Simplified Management:** Centralized certificate management through a single load balancer simplifies operations and maintenance tasks.

---

# Lesson 79. Connection Draining

### Understanding Connection Draining

**Connection draining** is a critical feature for maintaining good user experience during instance maintenance or scaling operations.

**Alternative Names:** On AWS, this process is also known as "deregistration delay" for newer load balancers like ALB and NLB.

### The Problem Connection Draining Solves

**Graceful Instance Removal:** When you're deregistering an instance (removing it from the load balancer pool) because it's unhealthy or you're scaling down, you don't want to abruptly cut off ongoing connections, as this would create a poor user experience.

### How Connection Draining Works

### Graceful Request Completion

**In-Flight Request Handling:** When an instance is being removed, connection draining allows any in-flight requests to that EC2 instance to complete naturally.

**New Request Prevention:** The load balancer stops sending new requests to the instance that's being removed, but waits for active requests to finish processing.

### Configurable Timing

**Flexible Duration:** You can control how long this process takes, with settings ranging from 1 second to 3600 seconds (1 hour).

**Default Setting:** The default duration is 300 seconds (5 minutes), which works well for most applications.

### Customisation Based on Application Needs

### Short-Duration Requests

**Quick Scaling:** If your traffic consists of short requests (like simple API calls), you can set a low value to speed up the deregistration process.

**Immediate Cutoff:** You can even set the value to zero if you want to cut off connections instantly, though this isn't recommended for production environments.

### Long-Running Requests

**Extended Processing:** For applications with long-running requests or when maintaining smooth user experience during scaling operations is critical, connection draining ensures users don't get interrupted.

### User Experience Benefits

**Seamless Transitions:** This feature is essential for maintaining service quality during scaling events, ensuring that users don't experience failed requests or interrupted sessions when instances are being removed from service.

**Automatic Management:** The load balancer handles this process automatically, requiring no manual intervention once configured properly.

### Load Balancer Variations

**Naming Differences:**

- **Classic Load Balancer:** Called "connection draining"
- **Application Load Balancer and Network Load Balancer:** Called "deregistration delay"

Both terms refer to the same concept of gracefully handling connections during instance removal.

---

# Lesson 80. What is an Auto Scaling Group?

### Understanding Auto Scaling Groups (ASG)

**Auto Scaling Groups** are incredibly useful for managing websites and applications where traffic can change dramatically at any time. In the cloud, scaling resources up or down is fast and easy, which is exactly what ASGs help automate.

### Primary ASG Functions

### Dynamic Instance Management

**Load-Based Scaling:** The primary goal of an ASG is to adjust the number of running EC2 instances based on current load conditions.

**Scale Out:** When traffic increases, the ASG adds more EC2 instances to keep up with demand.

**Scale In:** When load decreases, the ASG removes extra instances you no longer need, ensuring you don't pay for unused resources.

### Capacity Management

**Minimum Instances:** ASG ensures you always have a minimum number of instances running, even during low-traffic periods.

**Maximum Limits:** You can enforce a maximum number of instances so the system doesn't spin up too many, controlling costs.

### Advanced Features

### Load Balancer Integration

**Automatic Registration:** ASGs can automatically register new instances with your load balancer, ensuring traffic distribution includes new instances immediately.

### Health Management

**Instance Replacement:** If an instance becomes unhealthy or gets terminated, the ASG automatically recreates it, maintaining your desired capacity.

### Cost Benefits

**Free Service:** ASGs themselves are free; you only pay for the EC2 instances they manage, making them a cost-effective way to manage dynamic infrastructure.

### Business Value

**Operational Efficiency:** ASGs eliminate the need for manual scaling decisions, providing automatic response to changing demand patterns while optimising costs through dynamic resource allocation.

---

# Lesson 81. Auto Scaling Group Configuration

### ASG Capacity Management

Auto Scaling Groups operate based on three key capacity settings that define how your infrastructure scales.

### Capacity Configuration

### Minimum Capacity

**Baseline Instances:** The least number of EC2 instances you always want running, even during low-traffic periods. This ensures your application maintains basic availability and performance.

### Desired Capacity

**Target Instance Count:** Your target number of instances for normal load conditions. The ASG tries to maintain this number of instances unless demand changes require scaling.

### Maximum Capacity

**Scaling Limit:** The most instances you allow the ASG to scale up to during high-traffic periods. This prevents excessive costs by capping the number of instances that can be launched.

### Scaling Operations

### Scale Out (Adding Instances)

**Demand Response:** When traffic or demand increases, the ASG scales out by adding more instances up to the maximum capacity to handle the increased load.

**Performance Maintenance:** This ensures your application continues performing well even during traffic spikes.

### Scale In (Removing Instances)

**Cost Optimisation:** When traffic decreases, the ASG scales in by reducing the number of running instances to save costs, but never goes below the minimum capacity.

**Automatic Cost Management:** This automatic scaling ensures you're not paying for resources you don't need while maintaining service availability.

### Dynamic Infrastructure Benefits

**Responsive Architecture:** This scaling approach ensures your application runs smoothly during busy periods while automatically saving money when demand drops, creating an efficient, cost-effective infrastructure that adapts to real-world usage patterns.

---

# Lesson 82. Auto Scaling Group with Load Balancer Integration

### Complete Scalable Architecture

Let's examine how ASG and load balancers work together to create a dynamic, scalable, and highly available system.

### Traffic Flow Components

### User Traffic

**Application Access:** Users send traffic to your application, whether it's a website, mobile app, or any service running on AWS.

### Elastic Load Balancer (ALB)

**Traffic Distribution:** The ALB distributes incoming traffic across your EC2 instances, spreading the load so no single instance becomes overwhelmed.

**Health Monitoring:** ALB continuously checks the health of your EC2 instances, stopping traffic to unhealthy instances and routing it only to functional ones.

### Auto Scaling Group

**Dynamic Scaling:** ASG automatically adjusts the number of EC2 instances to match current load conditions.

**Scaling Examples:**

- **High Traffic:** During heavy website traffic (like sales events), ASG scales out by adding more instances
- **Low Traffic:** When traffic decreases, ASG scales in by reducing instances to save costs


### Integration Benefits

### Automated Health Management

**Comprehensive Monitoring:** ALB monitors instance health and reports to ASG, which can replace unhealthy instances automatically.

**Seamless Recovery:** If ALB detects an issue with an instance, it routes traffic away from the faulty instance until ASG replaces it or it recovers.

### Custom AMI Integration

**Rapid Deployment:** You can create custom Amazon Machine Images (AMIs) with pre-configured software. When ASG scales out, new instances launch using this AMI, meaning each new instance is immediately ready with your configurations.

**Consistent Environment:** This ensures all instances have identical software configurations, reducing deployment time and potential configuration errors.

### Production Architecture Benefits

**Real-World Application:** This setup is extremely common and valuable in production environments because it provides:

- **Automatic scaling** based on actual demand
- **High availability** through multi-instance architecture
- **Cost optimisation** through dynamic resource management
- **Operational simplicity** through automation

**Comprehensive Solution:** The combination of load balancing, auto scaling, and custom AMIs creates a robust, self-managing infrastructure that can handle varying loads while maintaining performance and controlling costs.

---

# Lesson 83. Auto Scaling Group Attributes

### Launch Templates vs Launch Configurations

**Modern Approach:** When creating ASGs, launch templates play a crucial role. Launch configurations (the older approach) are being phased out, so we primarily use launch templates now.

**Consistency Assurance:** These templates ensure that when your ASG adds or removes EC2 instances, they're configured with identical settings.

### Key Template Attributes

### AMI and Instance Type

**Image Configuration:** The AMI (Amazon Machine Image) is your pre-configured template that ensures each EC2 instance launched has the same software setup and configuration.

**Resource Specification:** Instance type defines the computational power of your machines (like t2.micro for basic needs, or compute-optimised, memory-optimised, storage-optimised instances for specific workloads).

### EC2 User Data

**Startup Automation:** This optional feature allows you to include scripts that run when an instance starts, handling startup tasks like installing packages or configuring software automatically.

**Consistent Deployment:** User data ensures every new instance follows the same setup process, maintaining consistency across your infrastructure.

### Storage Configuration

**EBS Volumes:** These are Elastic Block Store volumes providing persistent storage for your instances. You can specify the size, type, and configuration of storage each instance should have.

**Data Persistence:** EBS volumes ensure your instances have the storage capacity and performance characteristics your applications require.

### Security Configuration

**Network Security:** Security groups act as virtual firewalls controlling inbound and outbound traffic to your EC2 instances.

**Access Control:** These define which ports are open, which IP addresses can connect, and what protocols are allowed, ensuring consistent security policies across all scaled instances.

### SSH Key Pairs

**Remote Access:** SSH key pairs enable secure remote access to your instances for management and troubleshooting purposes.

**Consistent Access:** Including key pair configuration in launch templates ensures all instances can be accessed using the same authentication method.

### Template Benefits

**Infrastructure as Code:** Launch templates provide a declarative way to define your instance configuration, ensuring consistency, repeatability, and easy management of your scaling infrastructure.

**Version Control:** Templates can be versioned, allowing you to track changes and roll back to previous configurations if needed.

---

# Load Balancing \& Scalability Key Takeaways

### Scalability Fundamentals

- **Vertical scaling (scaling up)** increases power of existing instances but has hardware limits
- **Horizontal scaling (scaling out)** adds more instances for better resilience and unlimited growth
- **High Availability** ensures system uptime across multiple locations and failure scenarios
- **Elasticity** provides dynamic scaling based on actual demand patterns


### Load Balancer Types and Use Cases

- **Application Load Balancer (ALB)** for HTTP/HTTPS traffic with intelligent routing at Layer 7
- **Network Load Balancer (NLB)** for high-performance TCP/UDP traffic with ultra-low latency
- **Classic Load Balancer (CLB)** legacy option with limited features, avoid for new projects
- **Gateway Load Balancer (GLB)** for advanced networking and third-party appliance integration


### SSL/TLS Security Implementation

- **Certificate management** through AWS Certificate Manager or custom certificates
- **SNI (Server Name Indication)** enables multiple certificates on modern load balancers
- **Connection draining** ensures graceful instance removal without user disruption
- **Sticky sessions** maintain user affinity when session data isn't shared across instances


### Auto Scaling Group Management

- **Dynamic capacity adjustment** with minimum, desired, and maximum instance settings
- **Launch templates** define consistent instance configurations for scaling operations
- **Load balancer integration** provides automatic health monitoring and traffic distribution
- **Cost optimisation** through automatic scaling based on actual demand


### Security Group Configuration

- **Load balancer security groups** allow internet traffic on ports 80/443
- **Application security groups** restrict access to load balancer sources only
- **Layered security** protects backend instances from direct internet access
- **Traffic flow control** ensures secure, managed access to applications


### Best Practices

- **Use newer generation load balancers** (ALB/NLB) for enhanced features and SNI support
- **Implement health checks** at appropriate intervals for reliable traffic management
- **Configure appropriate scaling policies** based on application characteristics and traffic patterns
- **Plan for certificate renewal** to avoid service disruptions from expired SSL certificates
- **Design for failure** with multi-AZ distribution and automatic recovery mechanisms

These concepts form the foundation of scalable, highly available AWS architectures, enabling applications to handle varying loads while maintaining performance, security, and cost efficiency.

<div style="text-align: center">⁂</div>

[^1]: paste.txt


