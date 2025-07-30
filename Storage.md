# AWS Storage – Comprehensive DevOps Notes

---


## Lesson 53. What's an EBS Volume

### Understanding EBS Volumes

**EBS (Elastic Block Store) volumes** are network drives that you can attach to your EC2 instances. It's important to understand that these aren't physical drives like those in a laptop, but they function in a similar way as virtual storage devices that live in the cloud and connect to your instances.

### Key EBS Characteristics

### Data Persistence

**Persistent Storage:** One of the primary benefits of EBS is that it allows your instances to persist data. Even if you stop or terminate your instance, the data on the EBS volume remains intact (unless you specifically choose to delete it).

### Availability Zone Binding

**AZ Restrictions:** EBS volumes are bound to a specific Availability Zone. You cannot move a volume directly across zones, but you can create snapshots of the volume and use those snapshots to create new volumes in different zones when needed.

### How EBS Works

Think of EBS volumes like a USB drive that you can plug into your EC2 instance. You store your data on it, and even if you unplug it (stop your instance), that data remains safely stored on the virtual drive. You can then reconnect it to the same instance or attach it to another instance within the same Availability Zone later.

### Why Use EBS?

### Data Persistence Benefits

**Long-term Storage:** EBS is ideal for situations where you need to store data over extended periods, such as databases, application logs, or important files. Your data stays safe even if you terminate the instance it's attached to.

### Free Tier Offering

**Cost-Effective Testing:** AWS provides 30 GB of free EBS storage per month for general purpose SSD or magnetic storage types. This makes it excellent for experimentation and learning without incurring costs.

### Use Cases

EBS volumes are particularly useful for:

- Database storage requiring persistent data
- Application logs that need to survive instance restarts
- File systems that require consistent, reliable storage
- Any scenario where data must persist beyond the instance lifecycle


### Storage Integration

EBS provides a reliable storage option that works seamlessly with your EC2 instances, bridging the gap between temporary instance storage and permanent data requirements.

---


## Lesson 54. AMI Overview

### What is an AMI?

**AMI (Amazon Machine Image)** is essentially a blueprint for launching EC2 instances. An AMI is a pre-configured template containing all the information needed to launch and run an instance, including the operating system, software applications, configuration settings, monitoring tools, and other customisations.

### Why AMIs are Important

### Instance Customisation

**Pre-packaged Solutions:** AMIs represent a customisation of an EC2 instance, allowing you to pre-package everything your instance needs to boot up and run properly.

### Time and Efficiency Savings

**Automated Setup:** Instead of manually configuring everything each time you launch an instance, you can use an AMI to save significant time. All the software, configuration, and settings you need are pre-installed in the AMI, so when your instance launches, it's immediately ready for use.

**Faster Boot Times:** This approach results in faster boot times and eliminates time spent on repetitive manual setup tasks.

### AMI Distribution and Usage

### Regional Binding

**Region-Specific:** AMIs are built for specific regions, but you can copy them across regions when needed for multi-region deployments.

### Types of AMIs

### Public AMIs

**AWS-Provided:** These are provided by AWS and available for everyone to use. AWS offers public AMIs for popular operating systems including Ubuntu, Amazon Linux, Windows Server, and many others.

### Custom AMIs

**User-Created:** You can create your own AMI based on instances you've customised. This is particularly valuable for replicating specific setups across multiple instances and environments, ensuring consistency and reducing configuration drift.

### Marketplace AMIs

**Third-Party Solutions:** These AMIs are provided by third parties through the AWS Marketplace. Software vendors often offer pre-configured AMIs with their applications ready to use. Some are free while others require payment.

### AMI Benefits

### Infrastructure Automation

**Consistent Deployments:** AMIs make infrastructure management easier by allowing you to automate the setup of EC2 instances. Once you've created an AMI with your desired configuration, you can launch multiple instances with identical configurations.

### Scaling and Replication

**Template Functionality:** Think of AMIs as templates for launching instances. You can take snapshots of configured instances and create AMIs, enabling you to spin up identical instances across different environments.

**Enterprise Applications:** This capability is especially useful when scaling infrastructure or launching instances in different regions for global applications.

### Quality Assurance

**Reduced Human Error:** In complex environments and large-scale setups, using AMIs helps ensure every instance launches with exactly the same configuration, significantly reducing the chances of human error during setup processes.

**Environment Consistency:** AMIs guarantee that development, testing, and production environments can maintain consistent configurations.

---


## Lesson 55. Amazon EFS - Elastic File System

### What is Amazon EFS?

**EFS (Elastic File System)** is Amazon's managed solution for shared file storage. It's a managed network file system that allows you to create shared file storage that can be mounted across multiple instances simultaneously.

Think of EFS like a network drive that all your instances can access at the same time, similar to shared drives in office environments.

### How EFS Works

### Multi-AZ Architecture

**High Availability Design:** EFS is designed to work with EC2 instances in multi-Availability Zone setups. Data stored in EFS is highly available and redundant across different AZs, providing the reliability needed for critical applications.

**Automatic Replication:** Your data is automatically replicated across multiple locations for durability, ensuring business continuity even if individual components fail.

### Automatic Scaling

**Dynamic Growth:** One of EFS's key advantages is that it scales automatically as you add more data. You don't need to worry about provisioning storage capacity or manually resizing storage volumes as your needs grow.

### EFS Integration with EC2

### Multi-Instance Mounting

**Shared Access:** EFS can be mounted on multiple EC2 instances simultaneously. This builds upon concepts from Linux system administration where external file systems can be mounted using NFS (Network File System).

**Managed NFS:** With EFS, you get a fully managed version where you can mount the same file system across multiple instances, making it straightforward to share data between them.

### Practical Use Cases

**Content Management Systems:** EFS is particularly useful when running multiple instances of the same application that need access to shared files, such as content management systems or distributed workloads.

**Web Server Farms:** Multiple web servers can share the same content files, ensuring consistency across all instances.

### Cost Considerations

### Price Trade-offs

**Premium Pricing:** The main drawback of EFS is cost. It's approximately three times more expensive than standard general purpose SSD storage (GP2).

**Value Proposition:** While EFS is highly available and scalable, it's best to use it only when your application truly requires shared storage across multiple instances.

### When to Use EFS

### Appropriate Scenarios

EFS is an excellent solution when you need:

- Scalable, highly available file systems
- Shared storage accessible across multiple EC2 instances
- Multi-AZ distributed applications
- Content that must be consistently available across multiple servers


### Cost-Conscious Implementation

**Strategic Usage:** Be mindful of costs and implement EFS only when the shared storage functionality is essential to your application architecture.

### Linux Integration

**Familiar Mounting Process:** EFS works similarly to traditional Linux file system mounting. Once you set up EFS, you can mount it on each instance just like any other file system, making it familiar to system administrators with Linux experience.

## Storage Key Takeaways

### EBS Volume Fundamentals

- **Network-attached persistent storage** that survives instance termination
- **Availability Zone specific** with snapshot capability for cross-AZ mobility
- **30 GB free tier** monthly allowance for cost-effective learning and testing
- **Ideal for databases, logs, and persistent application data**


### AMI Management

- **Blueprint templates** containing complete instance configurations
- **Regional deployment** with cross-region copying capabilities
- **Multiple sources** including public, custom, and marketplace options
- **Automation and consistency** benefits for large-scale deployments


### EFS Capabilities

- **Shared network file system** accessible by multiple instances simultaneously
- **Multi-AZ redundancy** with automatic scaling capabilities
- **Premium pricing** approximately 3x standard SSD costs
- **Best for applications requiring shared storage** across distributed instances


### Storage Selection Strategy

- **EBS for persistent instance storage** requiring data survival beyond instance lifecycle
- **AMIs for deployment consistency** and rapid instance provisioning
- **EFS for shared storage requirements** across multiple instances with high availability needs


### Best Practices

- **Cost optimisation** through appropriate storage type selection based on actual requirements
- **Snapshot management** for EBS volumes to enable backup and cross-zone mobility
- **AMI standardisation** to ensure consistent deployments and reduce configuration errors
- **Strategic EFS implementation** only when shared storage functionality justifies the premium cost

These storage options provide the foundation for reliable, scalable data management in AWS environments, each serving specific use cases while offering different trade-offs between cost, performance, and functionality.


