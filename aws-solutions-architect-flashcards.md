### IAM:
Manages access to AWS resources using policies and identities (users, groups, roles).
IAM is global and free.

### IAM Users:
Represents a person or application with long-term credentials to interact with AWS.
Avoid using root user; assign least privilege access to IAM users.

### IAM Groups:
Collection of IAM users; simplifies permission management by attaching policies to the group.
A user can belong to multiple groups.

### IAM Policies:
JSON documents that define permissions (allow or deny) to AWS services.
Attach policies to users, groups, or roles.

### IAM MFA (Multi-Factor Authentication):
Adds an extra layer of security using an OTP device (e.g., app or hardware).
Recommended for root user and privileged accounts.

### Access Keys:
Consist of an access key ID and secret used for programmatic access via CLI or SDK.
Rotate keys regularly and avoid embedding them in code.

### IAM Organizations:
Centrally manage and govern multiple AWS accounts under one organization.
Use Service Control Policies (SCPs) to restrict what member accounts can do.

### Resource-based Policies:
Resource-based policies are attached directly to resources (e.g., S3 bucket policy).

### IAM Roles:
IAM Roles allow temporary access and can be assumed by services, users, or other AWS accounts.
Use cross-account access with roles, not users.

### AWS Directory Services:
Connects AWS resources with on-premises Microsoft AD or creates a managed directory in the cloud.
Used with Amazon WorkSpaces, RDS for SQL Server, and single sign-on (SSO).

### AWS Control Tower:
Automates setup of secure, compliant multi-account AWS environments using best practices.
Uses Organizations, SCPs, and AWS Config behind the scenes.

### Amazon Cognito:
Provides user sign-up, sign-in, and access control to web and mobile apps.
Supports identity federation with social providers (e.g., Google, Facebook) and enterprise SAML.

### User Authentication:
Cognito User Pools manage users and authenticate them directly.
Supports multi-factor authentication and password policies.

### Identity Federation:
Cognito Identity Pools provide temporary AWS credentials via federated identity providers.
Grants users temporary access to AWS services.

### SDKs:
Language-specific libraries (Python, Java, etc.) to interact with AWS services programmatically.
Requires proper IAM permissions and usually access keys or temporary credentials.

### CLI (Command Line Interface):
Tool to control AWS services from the terminal.
Configure with aws configure to set region, access key, and secret key.

### AWS CloudShell:
Browser-based shell with pre-installed tools to run CLI commands without local configuration.
Automatically uses the permissions of the IAM user signed into the console.

### EC2 User Data:
Script that runs automatically at the first boot of an EC2 instance.
Used to automate setup tasks like installing software or pulling configuration files.

### Region:
A geographical area containing multiple isolated Availability Zones.
Services are deployed per region; choose the region closest to your users.

### Availability Zone (AZ):
One or more isolated data centers within a region.
Use multiple AZs for high availability and fault tolerance.

### VPC (Virtual Private Cloud):
A logically isolated section of the AWS cloud where you can define your own networking environment.
Customize IP ranges, subnets, route tables, and gateways.

### Subnet:
A range of IP addresses within a VPC; used to group resources.
Public subnets have internet access; private subnets do not unless routed via NAT.

### CIDR (Classless Inter-Domain Routing):
Defines the IP address range of your VPC or subnet (e.g., 10.0.0.0/16).
Plan IP ranges carefully to avoid overlaps, especially for VPC peering.

### Security Groups:
Virtual firewalls at the instance level that control inbound and outbound traffic using allow-only rules.
Stateful; return traffic is automatically allowed.

### Network ACLs (NACLs):
Subnet-level stateless firewalls with allow and deny rules.
Used for fine-grained control over subnet traffic.

### Internet Gateway:
Enables communication between resources in your VPC and the internet.
Must be attached to the VPC and route table to work.

### Route Table:
Defines how traffic is directed within the VPC (e.g., to IGW, NAT, or VPC peering).
Each subnet must be explicitly associated with a route table.

### Bastion Host:
A secure EC2 instance in a public subnet used to access private instances via SSH.
Minimize attack surface by locking down SSH access to only the bastion.

### NAT Gateway:
Provides internet access for instances in private subnets without exposing them to inbound traffic.
Managed service; scalable and highly available.

### NAT Instances:
EC2-based alternative to NAT Gateway with more control but less scalability.
Requires manual configuration and patching.

### Egress-Only Internet Gateway:
Provides IPv6-only instances in private subnets with outbound internet access.
Does not allow inbound internet connections.

### VPC Peering:
Connects two VPCs for private traffic using internal IP addresses.
No transitive peering—each connection must be directly configured.

### VPC Endpoints:
Allows private connections to AWS services without going through the internet.
Interface endpoints (powered by PrivateLink) or gateway endpoints (S3/DynamoDB).

### VPC Flow Logs:
Capture information about IP traffic going to and from network interfaces in your VPC.
Used for troubleshooting and compliance auditing.

### VPC Traffic Mirroring:
Captures and analyzes network traffic from EC2 instances.
Useful for deep packet inspection and threat analysis.

### Cluster Placement Group:
Packs instances close together for low latency and high throughput.
Ideal for HPC or tightly coupled apps.

### Spread Placement Group:
Distributes instances across different hardware to reduce correlated failures.
Use for critical workloads requiring maximum fault tolerance.

### Partition Placement Group:
Spreads instances across partitions (sets of racks); reduces impact of rack failure.
Best for distributed systems like HDFS and Cassandra.

### Site-to-Site VPN:
Creates an encrypted IPsec VPN tunnel between your VPC and your on-premises network over the internet.
Used for quick, secure connectivity without dedicated lines.

### Virtual Private Gateway (VGW):
A VPN concentrator on the AWS side that connects your VPC to a Site-to-Site VPN or Direct Connect.
You attach a VGW to your VPC to enable external connectivity.

### Customer Gateway (CGW):
A representation of your on-premises VPN device in AWS used to establish the VPN connection.
Works with VGW to form the VPN tunnel; supports both static and dynamic routing.

### AWS Direct Connect:
Provides a dedicated, high-bandwidth, low-latency private connection between your on-premises data center and AWS.
Bypasses the public internet, improving performance and security.

### Direct Connect Gateway (DXGW):
Allows Direct Connect connections to access multiple VPCs across different AWS Regions.
Supports hybrid or multi-region architectures without creating multiple DX connections.

### Transit Gateway (TGW):
Acts as a central hub to connect multiple VPCs, VPNs, and DX connections using a hub-and-spoke model.
Simplifies complex network topologies; supports inter-region peering.

### CloudHub:
A legacy VPN-based solution that connects multiple remote networks to a single VGW in a hub-and-spoke design.
Works when multiple Customer Gateways connect to the same Virtual Private Gateway.

### AWS Database Migration Service (DMS):
Helps you migrate databases to AWS quickly and securely with minimal downtime.
Supports homogeneous (e.g., MySQL to MySQL) and heterogeneous (e.g., Oracle to Aurora) migrations.

### Common EC2 Ports:
Typical ports include 22 (SSH), 80 (HTTP), 443 (HTTPS), 3306 (MySQL), and 1433 (SQL Server).
Ensure security groups and NACLs are configured to allow only necessary ports.

### Spot Instances:
Use unused EC2 capacity at a reduced cost but may be interrupted by AWS.
Ideal for flexible, fault-tolerant workloads like batch jobs or CI/CD.

### Spot Fleet:
A collection of Spot and optionally On-Demand instances managed to meet desired capacity.
Allows diversified instance types and uses allocation strategies for cost optimization.

## EC2 Launch Types:

### Pay-as-you-go (On-Demand):
No commitment; pay per hour or second.

### Reserved Instances:
Long-term pricing discount for 1 or 3-year commitment.

### Spot Instance:
Cheapest option, but not reliable for persistent workloads.

### Dedicated Hosts:
Physical servers dedicated to your account for licensing and compliance.

### Dedicated Instances:
Run on hardware dedicated to you but may share with your other instances.

### EC2 Hibernate:
Saves the in-memory state of an EC2 instance to EBS and resumes from that snapshot.
Useful for fast reboots and workloads needing memory persistence.

### ENI (Elastic Network Interface):
A logical network interface attached to EC2 instances.
Used for high availability, failover, or attaching multiple IPs to an instance.

### EFA (Elastic Fabric Adapter):
High-performance networking for tightly coupled HPC applications.
Enables low-latency, high-bandwidth communication between instances.

### ENA (Elastic Network Adapter):
Supports enhanced networking with higher bandwidth and lower latency.
Provides up to 100 Gbps throughput on supported instance types.

### Auto Scaling Group (ASG):
Automatically adjusts the number of EC2 instances to meet application demand.
Helps maintain performance and optimize costs.

### Target Tracking Scaling:
Adjusts instance count to maintain a specified metric (e.g., CPU at 70%).
Most commonly used policy for dynamic and balanced scaling.

### Step Scaling:
Adds or removes instances in steps based on CloudWatch alarm thresholds.
Used when more granular control over scaling actions is needed.

### Simple Scaling:
Triggers scaling actions based on a single CloudWatch alarm.
Legacy option, now less commonly used compared to target tracking.

### Predictive Scaling:
Uses machine learning to forecast future demand and scale ahead of time.
Useful for recurring usage patterns like scheduled spikes.

### Serverless Architecture:
Lets you build and run applications without provisioning or managing servers.
Billing is based on usage, not uptime or provisioning.

### Lambda Function:
Runs code in response to triggers with automatic scaling and pay-per-use pricing.
Supports various runtimes and executes for up to 15 minutes per invocation.

### Lambda Limitations:
Maximum of 10 GB RAM, 15 minutes runtime, 250 MB deployment package, and 512 MB temporary storage.
Use Amazon EFS for larger or persistent storage needs.

### Lambda SnapStart:
Reduces cold starts by caching execution state for Java-based functions.
Improves startup time for latency-sensitive applications.

### Lambda@Edge:
Extends Lambda functions to AWS edge locations via CloudFront.
Ideal for customizing content close to end users.

### Lambda in VPC:
Allows Lambda to connect to private VPC resources like RDS and EC2.
Adds ENIs and may increase cold start time.

### API Gateway:
A fully managed service to create, publish, and manage APIs that connect to backend services.
Supports REST, HTTP, and WebSocket APIs with features like caching and throttling.

### Amazon ECS (Elastic Container Service):
Managed container orchestration service for Docker containers.
Supports EC2 and Fargate launch types for flexible deployments.

### ECS with Autoscaling:
Automatically adjusts ECS task count or EC2 capacity based on demand.
Can scale at both the container and infrastructure level.

### Amazon ECR (Elastic Container Registry):
Managed container image registry integrated with AWS services.
Simplifies storing, versioning, and deploying Docker images.

### Amazon EKS (Elastic Kubernetes Service):
Managed Kubernetes service to run and scale containerized apps.
Great for teams already using Kubernetes on-premises.

### EBS Snapshots:
Point-in-time backups of EBS volumes stored in S3.
Can be used to create new volumes or restore existing ones.

## EBS Volume Types:

### gp2 (General Purpose SSD):
Balanced price/performance for most workloads.
Baseline performance with burst capability based on volume size.

### io1/io2 (Provisioned IOPS SSD):
High-performance SSD for critical, I/O-intensive applications.
Supports provisioned IOPS with higher durability (io2).

### sc1 (Cold HDD):
Low-cost magnetic storage for infrequently accessed data.
Suitable for throughput-oriented workloads.

### st1 (Throughput-Optimized HDD):
Magnetic storage for frequently accessed, large sequential workloads.
Ideal for big data, log processing, and data warehouses.

### EC2 Instance Store:
Temporary block-level storage physically attached to the host machine.
Data is lost when the instance stops or terminates.

### Amazon S3:
Object storage built to store and retrieve any amount of data from anywhere.
Provides high durability (99.999999999%) and scalable performance.

### S3 Bucket Policy:
JSON-based policy to manage access at the bucket level.
Used to allow or deny actions for users, roles, or services.

## S3 Storage Classes:

### S3 Standard:
Default class for frequently accessed data.
High availability and low latency.

### S3 Standard-IA (Infrequent Access):
Lower-cost option for less frequently accessed data.
Retrieval costs apply.

### S3 One Zone-IA:
Like Standard-IA but stored in one AZ.
Lower cost but less availability.

### S3 Intelligent Tiering:
Automatically moves data between frequent and infrequent access tiers.
Ideal for unknown or changing access patterns.

### S3 Glacier:
Low-cost archival storage with retrieval in minutes to hours.
Suitable for compliance archives.

### S3 Glacier Deep Archive:
Lowest-cost option for rarely accessed data.
Retrieval can take up to 12 hours.

### Glacier Vault Lock:
Enforces compliance controls on Glacier vaults using WORM (Write Once Read Many).
Prevents data from being altered once locked.

### S3 Event Notifications:
Triggers Lambda, SNS, or SQS when specific events occur (e.g., object upload).
Useful for automating workflows.

### S3 Requester Pays:
Shifts the cost of access to the requester instead of the bucket owner.
Used in data-sharing models.

### S3 Lifecycle Rules:
Automates moving or deleting objects based on rules (e.g., move to Glacier after 30 days).
Helps optimize storage costs.

### S3 Website Hosting:
Enables hosting static websites directly from an S3 bucket.
Supports custom error pages and routing rules.

### S3 Versioning:
Maintains multiple versions of an object for recovery and rollback.
Must be explicitly enabled on the bucket.

### S3 Replication:
Copies objects across buckets (same or cross-region) for redundancy.
Requires versioning to be enabled.

### S3 Object Lock:
Prevents deletion or overwrite of objects for a specified time.
Used to enforce compliance requirements.

### S3 Batch Operations:
Perform actions on billions of S3 objects with a single request.
Supports copying, tagging, ACL updates, and Lambda invocation.

### S3 MFA Delete:
Adds a layer of protection by requiring MFA to delete objects or change versioning.
Can only be enabled via the CLI.

### S3 CORS (Cross-Origin Resource Sharing):
Controls how S3 can be accessed from different domains.
Used in web applications needing cross-domain access.

### S3 Default Encryption:
Automatically encrypts new objects using SSE-S3 or SSE-KMS.
Applies encryption at the bucket level.

### S3 Access Logs:
Logs detailed access requests for audit and analysis.
Can be stored in another bucket for review.

### S3 Pre-signed URLs:
Grants temporary access to specific objects using time-limited URLs.
Commonly used for secure, limited-time downloads.

### S3 Access Points:
Create custom access configurations for shared data sets.
Allows different permissions for different applications or users.

### S3 Transfer Acceleration:
Speeds up uploads using AWS edge locations.
Improves transfer speeds over long distances or for global users.

### S3 Multipart Upload:
Splits large files into parts for faster, parallel uploading.
Improves performance and reliability for large objects.

### S3 Encryption – At Rest and In Transit:
AWS encrypts data in transit using HTTPS and provides multiple options to encrypt data at rest.
You can enforce encryption using bucket policies, default encryption, or specific encryption methods.

### Server-Side Encryption (SSE):
AWS handles both key management and encryption operations on the server side.
Simplifies encryption but limits control compared to client-side options.

### SSE-S3:
AWS manages the encryption key and uses AES-256 encryption automatically.
No user interaction with keys; easiest to implement.

### SSE-KMS:
AWS Key Management Service handles key management and logging for additional control.
Allows user-managed keys and audit trails via CloudTrail.

### SSE-C:
You supply your own encryption key; AWS performs encryption using the provided key.
You must manage keys; AWS does not store them.

### Client-Side Encryption:
Data is encrypted by the client before being uploaded to S3.
Gives full control but adds development complexity.

### SSL Certificates (HTTPS):
Secure communication using TLS encryption between clients and AWS services.
Ensures data confidentiality in transit for web-facing apps.

### AWS ACM (Certificate Manager):
Automatically provisions, renews, and deploys SSL/TLS certificates.
Used with services like ELB, CloudFront, and API Gateway for HTTPS.

### Amazon EFS (Elastic File System):
Scalable, serverless NFS file storage that grows and shrinks automatically.
Used for Linux-based workloads with shared access across multiple EC2 instances.

### AWS Transfer Family:
Fully managed service for transferring files using SFTP, FTPS, and FTP to S3 or EFS.
Supports migration of legacy file transfer workloads to the cloud.

### Amazon FSx:
Provides managed file systems optimized for specific workloads (e.g., Windows File Server, Lustre, NetApp ONTAP).
Great for applications needing native file protocols and performance tuning.

### AWS Storage Gateway – Tape Gateway:
Virtual tape library that integrates with backup software and stores data in Glacier.
Replaces physical tape infrastructure with cloud-based storage.

### AWS Storage Gateway – Block Storage Gateway:
Provides block storage volumes to on-premises apps, backed by S3.
Useful for extending local storage capacity and disaster recovery.

### AWS DataSync:
Automates fast, secure data transfers between on-premises storage and AWS services.
Handles large-scale migrations and recurring transfers with scheduling and verification.

### AWS Snow Family:
A set of physical devices used to move large amounts of data into or out of AWS when network transfer is impractical.
Useful for edge computing, offline migrations, and disconnected environments.

### Snowcone:
Small, portable edge device (8 TB usable storage) designed for lightweight data collection and edge processing.
Battery-powered and suitable for remote or space-constrained environments.

### Snowball Edge:
Ruggedized device (up to 80 TB) with compute and storage capabilities.
Supports EC2 instances and Lambda for edge computing; used for large data transfers and edge applications.

### Snowmobile:
Exabyte-scale data transfer service using a shipping container-sized device.
Designed for massive migrations, such as entire data center moves to AWS.

### DNS (Domain Name System):
Resolves human-readable domain names into IP addresses.
AWS uses Route 53 as its highly available and scalable DNS service.

### Route 53 Health Checks:
Monitor the health of endpoints to route traffic only to healthy resources.
Can be attached to records or used independently for alarms and failover.

### TTL (Time to Live):
Defines how long DNS resolvers cache a record before refreshing it.
Shorter TTLs allow for faster changes but increase DNS traffic.

## Routing Policies in Route 53:

### Simple Routing:
Returns one record with no health check or logic.
Used for single-resource domains.

### Weighted Routing:
Routes traffic proportionally based on defined weights.
Used for A/B testing or gradual deployments.

### Latency-Based Routing:
Routes users to the region with the lowest latency.
Improves performance by directing traffic to the closest endpoint.

### Failover Routing:
Routes to a secondary resource when the primary is unhealthy.
Requires health checks for the primary.

### Geolocation Routing:
Routes traffic based on the user's geographic location.
Useful for complying with regional laws or content localization.

### Multivalue Answer Routing:
Returns multiple healthy records with optional health checks.
Can act as a basic load balancer.

### CNAME (Canonical Name Record):
Maps one domain name to another.
Cannot be used for the root domain (e.g., example.com).

### Alias Record:
AWS-specific Route 53 feature that maps a domain to AWS resources (e.g., ELB, CloudFront).
Can be used at the root domain and is free of charge.

### Application Load Balancer (ALB):
Operates at Layer 7 (HTTP/HTTPS) and supports content-based routing.
Best for microservices and modern web apps using path- or host-based routing.

### Network Load Balancer (NLB):
Operates at Layer 4 (TCP/UDP) and provides ultra-low latency.
Suitable for high-performance and real-time applications.

### Gateway Load Balancer (GLB):
Distributes traffic across third-party virtual appliances.
Commonly used for security appliances like firewalls and intrusion detection systems.

### ELB Sticky Sessions:
Binds a user session to a specific target for session persistence.
Useful for stateful applications needing consistent backend access.

### Cross-Zone Load Balancing:
Distributes traffic evenly across all targets in all enabled AZs.
Helps improve fault tolerance and target utilization.

### CloudFront:
AWS content delivery network (CDN) that caches and distributes content via edge locations.
Improves global performance and integrates with S3, ALB, and Lambda@Edge.

### CloudFront Georestriction:
Restricts access to content based on the viewer’s geographic location.
Used to comply with licensing or regulatory requirements.

### AWS Global Accelerator:
Optimizes routing and improves global application availability using the AWS global network.
Uses static IP addresses and intelligent routing to the nearest healthy AWS region.

### RDS Read Replicas:
Provide read scalability by asynchronously replicating data from a primary database.
Useful for offloading read-heavy workloads.

### RDS Multi-AZ:
Provides high availability with synchronous standby replica in a different Availability Zone.
Automatic failover in case of primary instance failure.

### RDS Security:
Supports encryption at rest using KMS, encryption in transit via SSL, IAM authentication, and network isolation via VPC.
Security best practices include using security groups and parameter groups.

### RDS Proxy:
Managed database proxy to improve application availability and scalability by pooling connections.
Helps reduce database overload and failover times.

### RDS Custom:
Allows customization for Oracle and Microsoft SQL Server with access to the underlying OS.
Useful for legacy or specialized workloads requiring custom configurations.

### Amazon Aurora:
High-performance, MySQL and PostgreSQL-compatible relational database.
Offers up to 5x performance improvements over standard MySQL with built-in replication and fault tolerance.

### DynamoDB Global Tables:
Multi-region, fully replicated tables for low-latency access and disaster recovery.
Supports active-active replication with eventual consistency across regions.

### ElastiCache:
Fully managed in-memory caching service to improve application performance and reduce latency.
Supports two popular engines:
Memcached and Redis.

### Memcached:
Simple, multi-threaded, in-memory key-value store.
Best for simple caching scenarios, horizontally scalable but without persistence or advanced data structures.

### Redis:
Advanced, single-threaded, in-memory data store with persistence options.
Supports data structures like lists, sets, sorted sets, pub/sub messaging, transactions, and Lua scripting.

### DocumentDB:
Fully managed document database service compatible with MongoDB APIs.
Designed for JSON-based, semi-structured data.

### Neptune:
Managed graph database service optimized for highly connected datasets and graph queries.
Supports property graph and RDF graph models.

### Athena:
Serverless interactive query service using standard SQL on data stored in S3.
Great for ad-hoc analysis without infrastructure management.

### Redshift:
Fully managed petabyte-scale data warehouse service.
Optimized for complex queries and large data analytics.

### EMR (Elastic MapReduce):
Managed Hadoop and Spark service for big data processing.
Used for batch processing, machine learning, and analytics.

### QuickSight:
Scalable business intelligence service with interactive dashboards and visualizations.
Integrates with AWS data sources for real-time insights.

### Glue:
Fully managed ETL (extract, transform, load) service.
Automates data preparation and cataloging for analytics.

### Lake Formation:
Simplifies building secure data lakes on AWS.
Automates data ingestion, cataloging, and access control.

### MSK (Managed Streaming for Kafka):
Fully managed Apache Kafka service.
Used for building real-time data pipelines and streaming apps.

### Big Data Ingestion Pipeline:
Combination of services like Kinesis, MSK, Glue, and Data Pipeline to ingest, process, and analyze streaming and batch data.
Enables scalable, real-time analytics and machine learning workflows.

### Athena:
Serverless, interactive SQL query service for analyzing data directly in Amazon S3.
Ideal for ad-hoc querying without infrastructure setup.

### Redshift:
Fully managed, petabyte-scale data warehouse service.
Optimized for complex queries and fast analytics using columnar storage and MPP architecture.

### EMR (Elastic MapReduce):
Managed Hadoop and Spark platform for big data processing.
Used for batch processing, machine learning, and large-scale data transformations.

### QuickSight:
Cloud-native business intelligence and visualization service.
Creates interactive dashboards and supports machine learning insights.

### Glue:
Serverless ETL service that discovers, catalogs, and prepares data for analytics.
Automates data extraction, transformation, and loading tasks.

### Lake Formation:
Simplifies building, securing, and managing data lakes on AWS.
Manages data ingestion, access control, and cataloging centrally.

### MSK (Managed Streaming for Kafka):
Fully managed Apache Kafka service for real-time data streaming.
Supports building event-driven applications and streaming pipelines.

### SQS:
Fully managed message queuing service for decoupling components and buffering messages.
Supports standard (at-least-once delivery) and FIFO (exactly-once, ordered) queues.

### SQS Message Visibility Timeout:
Time period during which a received message is hidden from other consumers.
Prevents multiple consumers from processing the same message simultaneously.

## SQS Polling:

### Short Polling:
Returns immediately, may return empty if no messages available.

### Long Polling:
Waits up to 20 seconds for messages to arrive, reducing empty responses and costs.

### SQS FIFO Queues:
Guarantees exactly-once processing and preserves message order.
Ideal for workflows where order and duplication prevention matter.

### SNS:
Fully managed pub/sub messaging service for sending notifications to multiple subscribers.
Supports multiple protocols:
HTTP/S, email, SMS, Lambda, SQS, etc.

### SNS + SQS Fan-out Pattern:
SNS sends a single message to multiple SQS queues or endpoints.
Enables parallel processing and decoupling of consumers.

### Kinesis Data Streams:
Real-time streaming data service for building custom applications that process or analyze streaming data.
Supports high-throughput ingestion with shards and scaling.

### Kinesis Data Firehose:
Fully managed service for loading streaming data into AWS data stores like S3, Redshift, and Elasticsearch.
No need to write applications; automatically batches and delivers data.

### Kinesis Data Analytics:
Allows real-time SQL queries on streaming data from Kinesis Data Streams or Firehose.
Enables real-time insights without managing infrastructure.

### AWS WAF (Web Application Firewall):
Protects web apps from common web exploits like SQL injection and XSS.
Can be deployed on CloudFront, ALB, API Gateway, and supports custom rules.

### AWS Shield (DDoS Protection):
Protects applications from Distributed Denial of Service (DDoS) attacks.

### Shield 
Standard is automatic and free;

### Shield Advanced 
offers enhanced protection and 24/7 access to the DDoS Response Team (DRT).

### AWS Firewall Manager:
Centralized security management for AWS WAF, Shield Advanced, and security groups across multiple accounts.
Helps enforce organization-wide security policies using AWS Organizations.

### Amazon GuardDuty:
Threat detection service that continuously monitors AWS accounts and workloads for malicious activity.
Analyzes logs from CloudTrail, VPC Flow Logs, and DNS queries.

### Amazon Inspector:
Automated vulnerability management and security assessment service for EC2 and containers.
Identifies software vulnerabilities and unintended network exposure.

### Amazon Macie:
Data security service that uses machine learning to discover and protect sensitive data in S3 (like PII).
Useful for compliance with data privacy regulations like GDPR.

### CloudWatch Metrics:
Collects and stores real-time data points (metrics) from AWS services and custom applications.
Used for monitoring resource utilization and triggering alarms.

### CloudWatch Logs:
Captures and stores logs from AWS services, Lambda, and on-prem systems.
Useful for debugging, auditing, and analysis.

### CloudWatch Alarms:
Monitor CloudWatch metrics and trigger actions (e.g., SNS, Auto Scaling) when thresholds are breached.
Supports high/low threshold alarms and composite alarms.

### CloudWatch Agent & Logs Agent:

### CloudWatch Agent:
Collects system-level metrics and logs from EC2 or on-prem servers.

### Logs Agent:
Specifically collects log files from Linux servers (legacy).

### EventBridge:
Serverless event bus for routing events from AWS services, custom apps, or SaaS to targets.
Used for event-driven architecture and automation workflows.

### AWS CloudTrail:
Tracks all API calls and console actions across AWS services.
Essential for auditing, governance, and incident response.

### AWS Config:
Tracks configuration changes and evaluates AWS resources against compliance rules.
Provides a detailed inventory and history of AWS resources.

### Encryption in AWS:
Available for data at rest (e.g., S3, EBS, RDS) and in transit (e.g., TLS).
Often integrates with AWS KMS or customer-managed keys.

### AWS KMS (Key Management Service):
Manages encryption keys and supports usage logging with CloudTrail.
Allows creation of customer-managed and AWS-managed keys.

### KMS Multi-Region Keys:
Enables encrypted data replication across regions with cryptographic equivalence.
Helps in building multi-region DR and compliance strategies.

### Encrypted AMI Sharing:
Allows encrypted AMIs to be shared across accounts using KMS grants.
Useful for secure image distribution within organizations.

### S3 Replication with Encryption:
Supports cross-region replication of encrypted S3 objects using KMS keys.
Requires enabling versioning and permissions for KMS access.

### SSM Parameter Store:
Stores configuration data and secrets as plain text or encrypted values.
Integrates with EC2, Lambda, and other AWS services for secure config retrieval.

### AWS Secrets Manager:
Manages, rotates, and securely retrieves database credentials, API keys, and secrets.
Supports automatic rotation and fine-grained access control via IAM.

### RDS and Aurora Migrations:
Use Database Migration Service (DMS) to migrate RDS or on-prem databases to Amazon RDS or Aurora.
Supports homogeneous (e.g., MySQL → MySQL) and heterogeneous (e.g., Oracle → Aurora) migrations.

### AWS Backup:
Centralized backup service for automating backup scheduling and retention across AWS services (e.g., EBS, RDS, DynamoDB).
Supports compliance and disaster recovery strategies.

### Application Migration Service (MGN):
Automates lift-and-shift of physical, virtual, and cloud servers to AWS.
Keeps source servers running during replication to reduce downtime.

### VMware Cloud on AWS:
Enables running VMware workloads on dedicated AWS infrastructure.
Useful for extending data centers and migrating without re-architecting.

### AWS CloudFormation:
Infrastructure as Code (IaC) service that provisions AWS resources using YAML or JSON templates.
Supports automation, version control, and repeatable deployments.

### Amazon SES (Simple Email Service):
Scalable email sending service for transactional or marketing communications.
Supports SMTP and API-based email sending with domain authentication.

### Amazon Pinpoint:
Targeted marketing and analytics tool for sending email, SMS, push notifications, and voice messages.
Includes segmentation, analytics, and A/B testing capabilities.

### Amazon MQ:
Managed broker for Apache ActiveMQ and RabbitMQ.
Ideal for migrating existing message brokers without code changes.

### SSM Session Manager:
Provides secure shell access to EC2 instances without requiring open ports or bastion hosts.
Integrated with IAM and CloudTrail for auditing and access control.

### AWS Cost Explorer:
Visualizes and analyzes AWS usage and cost data.
Helps in budgeting, forecasting, and identifying cost optimization opportunities.

### AWS Batch:
Fully managed service for running large-scale batch computing jobs.
Dynamically provisions compute resources and integrates with EC2 and Spot Instances.

### Amazon AppFlow:
No-code/low-code service to automate data transfers between SaaS apps and AWS (e.g., Salesforce to S3).
Supports transformation and filtering during the data flow.

### AWS Amplify:
Front-end development platform for building full-stack web and mobile apps.
Supports hosting, GraphQL/REST APIs, CI/CD, and authentication via Cognito.

### AWS App Runner:
Fully managed service to deploy web applications and APIs directly from source code or container images.
Abstracts infrastructure and supports automatic scaling.

## AI/ML and Language Services

### Amazon Rekognition:
Image and video analysis service that detects objects, people, text, activities, and facial recognition.
Commonly used in security, media analysis, and content moderation.

### Amazon Transcribe:
Converts speech to text using automatic speech recognition (ASR).
Ideal for audio transcription, subtitles, and voice-driven applications.

### Amazon Polly:
Converts text into lifelike speech using neural text-to-speech (NTTS) technology.
Used for voice interfaces, accessibility tools, and media content.

### Amazon Translate:
Neural machine translation service for real-time, high-quality language translation.
Supports multilingual websites, apps, and content.

### Amazon Lex:
Build conversational interfaces (chatbots) using the same deep learning as Alexa.
Supports voice and text input with natural language understanding (NLU).

### Amazon Comprehend:
Natural language processing (NLP) service to extract meaning from text (e.g., sentiment, key phrases, entities).
Useful for document classification, customer feedback analysis, and search enhancement.

### Amazon Comprehend Medical:
Specialized NLP service to extract medical information from unstructured clinical text.
Helps healthcare providers and researchers process large volumes of health data.

### Amazon SageMaker:
Fully managed ML service to build, train, and deploy machine learning models at scale.
Supports Jupyter notebooks, built-in algorithms, model tuning, and inference endpoints.

### Amazon Forecast:
Time-series forecasting service built on machine learning.
Used for demand planning, inventory, and financial forecasting with minimal ML experience.

### Amazon Kendra:
Intelligent enterprise search service that uses natural language to search across internal documents.
Improves employee productivity by enabling smarter data discovery.

### Amazon Personalize:
ML service for building real-time personalized recommendations, similar to what Amazon.com uses.
Requires no ML expertise and integrates easily with applications.

### Amazon Textract:
Automatically extracts text, forms, and tables from scanned documents and PDFs.
Goes beyond simple OCR by preserving layout and structure.

### High Availability: 
Designing systems to be resilient to failures and ensure continuous operations.
Achieved using Multi-AZ deployments, load balancing, Auto Scaling, and fault-tolerant services like S3 and DynamoDB.

### Scalability: 
Ability to grow or shrink resources dynamically based on demand.

### Vertical scaling: 
Increasing instance size.

### Horizontal scaling: 
Adding/removing instances (e.g., EC2 + Auto Scaling Group).

### Cost Optimization: 
Managing resources efficiently to reduce AWS spending without compromising performance.
Use pricing models like Reserved Instances, Spot Instances, and services like S3 Intelligent Tiering or Compute Savings Plans.

### High Computing: 
For workloads requiring intensive CPU, memory, or GPU (e.g., machine learning, HPC, rendering).

### Connection Draining: 
Allows an Elastic Load Balancer to stop sending new requests to an EC2 instance while keeping existing connections alive until they finish.

### Synchronous Communication: 
The client sends a request and waits for the response before continuing.

### Asynchronous Communication: 
The client sends a request and proceeds without waiting for a response.