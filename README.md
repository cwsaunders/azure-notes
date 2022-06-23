# AWS to Azure comparison


# Subscriptions and Accounts
<b>Diagram 1:<br></b>
<img src="https://docs.microsoft.com/en-us/azure/architecture/aws-professional/images/azure-aws-account-compare.png"><br>

Azure subscriptions are a grouping of resources with an assigned owner responsible for billing and permissions management. Unlike AWS, where any resources created under the AWS account are tied to that account, subscriptions exist independently of their owner accounts, and can be reassigned to new owners as needed.<br><br>

<b>Account Administrator.</b> The subscription owner and the billing owner for the resources used in the subscription. The account administrator can only be changed by transferring ownership of the subscription. Only one Account administrator is assigned per Azure Account.<br><br>

<b>Service Administrator.</b> This user has rights to create and manage resources in the subscription, but is not responsible for billing. By default, for a new subscription, the Account Administrator is also the Service Administrator. The account administrator can assign a separate user to the service administrator for managing the technical and operational aspects of a subscription. Only one service administrator is assigned per subscription.<br><br>

<b>Co-administrator.</b> There can be multiple co-administrators assigned to a subscription. Co-administrators have the same access privileges as the Service Administrator, but they cannot change the service administrator.<br><br>

Link: https://docs.microsoft.com/en-us/azure/architecture/aws-professional/accounts

<br>

# Compute<br><br>

1. AWS EC2 == Azure VM
1. AWS EBS == Azure Storage for VM Disks
1. AWS Lambda == Azure Functions, Azure Web-Jobs, and Azure Logic Apps
1. AWS Autoscaling == Azure VM scaling, and Azure App Service Autoscale
1. AWS EKS == Azure Kubernetes Service
1. AWS AppMesh == Azure Service Fabric
1. AWS ECS == Azure Container Instances

Link: https://docs.microsoft.com/en-us/azure/architecture/aws-professional/compute<br><br>

# Databases

1. AWS RDS == SQL Database, Azure Database for MySQL, Azure Database for PostgreSQL, Azure Database for MariaDB
1. AWS Aurora == Azure SQL Database (https://docs.microsoft.com/en-us/azure/azure-sql/database/serverless-tier-overview?view=azuresql)
1. AWS DynamoDB / Amazon DocumentDB == Cosmos DB
1. AWS ElastiCache == Cache for Redis

# Networking

1. AWS ELB == Azure Load Balancer
1. AWS ALB == Azure Application Gateway
1. AWS Route53 == Azure DNS + Azure Traffic Manager
1. AWS DirectConnect == Azure ExpressRoute
1. AWS Route Tables == Azure User-Defined Routes
1. AWS Private Link == Azure Private Link
1. AWS VPC Peering == Azure VNet Peering
1. AWS CloudFront == Azure CDN
1. AWS VPC == Azure Virtual Network (VNet)
1. AWS NAT Gateway == Azure Virtual Network NAT
1. AWS VPN Gateway == Azure VPN Gateway
1. AWS VPC Endpoint == Azure Private Endpoint
1. AWS VPC Flow Logs == Azure Network Watcher

# Regions and Zones

Diagram 2:<br>
<img src="https://docs.microsoft.com/en-us/azure/architecture/resiliency/images/redundancy.svg"><br><br>

In Azure, a region is divided into two or more Availability Zones. An Availability Zone corresponds with a physically isolated datacenter in the geographic region. Azure has numerous features for providing application redundancy at every level of potential failure, including availability sets, availability zones, and paired regions.<br><br>

	                Availability Set	Availability Zone	Paired region 
    Scope of failure	Rack	        Datacenter	        Region
    Request routing	    Load Balancer	    Cross-zone Load Balancer	Traffic Manager
    Network latency	    Very low	        Low	                Mid to high
    Virtual networking	    VNet	        VNet	            Cross-region VNet peering

# Messaging services

1. AWS SES does not have an Azure equivalent, you need a third party solution. (e.g. SendGrid)
1. AWS SQS == Azure Queue Storage
1. AWS SNS == Azure Service Bus
1. AWS EventBridge == Azure Event Grid
1. AWS Kinesis == Event Hubs

# Resource Management

The term "resource" in Azure is used in the same way as in AWS, meaning any compute instance, storage object, networking device, or other entity you can create or configure within the platform.<br><br>

Both Azure and AWS have entities called "resource groups" that organize resources such as VMs, storage, and virtual networking devices. However, Azure resource groups are not directly comparable to AWS resource groups.<br><br>

<b><i>While AWS allows a resource to be tagged into multiple resource groups, an Azure resource is always associated with one resource group.</b></i> A resource created in one resource group can be moved to another group, but can only be in one resource group at a time. Resource groups are the fundamental grouping used by Azure Resource Manager.<br><br>

