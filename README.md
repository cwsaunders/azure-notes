# AWS to Azure comparison


# Subscriptions, Accounts, and Management Groups
<b>Diagram 1:<br></b>
<img src="https://docs.microsoft.com/en-us/azure/architecture/aws-professional/images/azure-aws-account-compare.png"><br>

Azure subscriptions are a grouping of resources with an assigned owner responsible for billing and permissions management. Unlike AWS, where any resources created under the AWS account are tied to that account, subscriptions exist independently of their owner accounts, and can be reassigned to new owners as needed.<br><br>

<b>Account Administrator.</b> The subscription owner and the billing owner for the resources used in the subscription. The account administrator can only be changed by transferring ownership of the subscription. Only one Account administrator is assigned per Azure Account.<br><br>

<b>Service Administrator.</b> This user has rights to create and manage resources in the subscription, but is not responsible for billing. By default, for a new subscription, the Account Administrator is also the Service Administrator. The account administrator can assign a separate user to the service administrator for managing the technical and operational aspects of a subscription. Only one service administrator is assigned per subscription.<br><br>

<b>Co-administrator.</b> There can be multiple co-administrators assigned to a subscription. Co-administrators have the same access privileges as the Service Administrator, but they cannot change the service administrator.<br><br>

Link: https://docs.microsoft.com/en-us/azure/architecture/aws-professional/accounts

<h2>Strategies:</h2><br>
1. Workload separation strategy:<br>
An organization often adds new workloads to the cloud. Different ownership of subscriptions or basic separation of responsibility might result in multiple subscriptions in both the production and nonproduction management groups. This approach provides basic workload separation. But it doesn't take good advantage of the inheritance model to automatically apply policies across a subset of your subscriptions.
<img src="https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/_images/ready/management-group-hierarchy-v2.png"><br><br>

2. Application category strategy:<br>
As an organization's cloud footprint grows, more subscriptions are typically created to support applications. These applications have fundamental differences in business criticality, compliance requirements, access controls, or data protection needs. Built from the initial production and nonproduction subscriptions, the subscriptions that support these application categories are organized under either the production or nonproduction management group as applicable. These subscriptions are typically owned and administered by the operations staff of a central IT team.<br>
<img src="https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/_images/decision-guides/decision-guide-subscriptions-hierarchy.png"><br>
Each organization categorizes their applications differently. They often separate subscriptions based on specific applications or services, or by application archetypes. This categorization is designed to support workloads that are likely to consume most of the resource limits of a subscription. It might also separate mission-critical workloads to ensure they don't compete with other workloads under these limits. Some workloads that might justify a separate subscription include:<br><br>

    1. Mission-critical workloads.
    2. Applications that are part of cost of goods sold (COGS) within your company. For example, every widget manufactured by a company contains an Azure IoT module that sends telemetry. This process might require a dedicated subscription for accounting or governance purposes to be part of COGS.
    3. Applications subject to regulatory requirements like HIPAA or FedRAMP.

3. Mix Subscription Strategies:<br>
Management group hierarchies can be up to six levels deep. This depth gives you the flexibility to create a hierarchy that combines several of these strategies to meet your organizational needs. For example, the following diagram shows an organizational hierarchy that combines a business unit strategy with a geographic strategy.<br>
<img src="https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/_images/decision-guides/decision-guide-subscriptions-hierarchy-mixed.png"><br>

Link: https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/decision-guides/subscriptions/
<br>

<h2>Creation/Policies:</h2><br>

When you define your management group hierarchy, first create the root management group. Then move all existing subscriptions in the directory into the root management group. New subscriptions always go into the root management group initially. Later, you can move them to another management group.<br><br>

What happens when you move a subscription to an existing management group? The subscription inherits the policies and role assignments from the management group hierarchy above it. Establish many subscriptions for your Azure workloads. Then create other subscriptions to contain Azure services that other subscriptions share.
<br><br>
Link: https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/organize-subscriptions
<br>

<br><b>Access by management group:</b><br>
Another scenario where you would use management groups is to provide user access to multiple subscriptions. By moving multiple subscriptions under that management group, you can create one Azure role assignment on the management group, which will inherit that access to all the subscriptions. One assignment on the management group can enable users to have access to everything they need instead of scripting Azure RBAC over different subscriptions.<br><br>

Each directory is given a single top-level management group called the root management group. The root management group is built into the hierarchy to have all management groups and subscriptions fold up to it. This root management group allows for global policies and Azure role assignments to be applied at the directory level. The Azure AD Global Administrator needs to elevate themselves to the User Access Administrator role of this root group initially. After elevating access, the administrator can assign any Azure role to other directory users or groups to manage the hierarchy. As administrator, you can assign your own account as owner of the root management group.<br><br>

<B>Restrictions:</b><br>
Management groups can support 6 levels of depth (not including root level or subscription level). Each management group and subscription can only support one parent.<br><br>

Azure custom role support for management groups is currently in preview with some limitations. You can define the management group scope in the Role Definition's assignable scope. That Azure custom role will then be available for assignment on that management group and any management group, subscription, resource group, or resource under it. This custom role will inherit down the hierarchy like any built-in role.<br><br>

Link: https://docs.microsoft.com/en-us/azure/governance/management-groups/overview<br><br>

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

<b><i>Resources can also be organized using tags.</b></i> Tags are key-value pairs that allow you to group resources across your subscription irrespective of resource group membership.<br><br>

Resources can be managed in these ways:<br>
1. Web interface
1. API
1. Command Line
1. PowerShell
1. Templates
<br>
<br>
Azure naming tool: https://github.com/microsoft/CloudAdoptionFramework/tree/master/ready/AzNamingTool

<br>

# Storage

1. AWS S3 == Azure Blob Storage
1. AWS EBS == Azure Managed Disks
1. AWS EFS == Azure Files
1. AWS S3 Infrequent Access == Azure Storage Cool Tier
1. AWS S3 Glacier == Azure Storage Archive access tier
1. AWS Backup == Azure Backup
1. AWS Storage Gateway == Azure StorSimple
1. AWS DataSync == Azure File Sync

# Azure Active Directory (AD/AAD)

<b>Azure AD Elevated Access:</b><br>
When you elevate your access, you will be assigned the User Access Administrator role in Azure at root scope (/). This allows you to view all resources and assign access in any subscription or management group in the directory. User Access Administrator role assignments can be removed using Azure PowerShell, Azure CLI, or the REST API.<br><br>

<img src="https://docs.microsoft.com/en-us/azure/role-based-access-control/media/elevate-access-global-admin/elevate-access.png">

<br><br>Link: https://docs.microsoft.com/en-us/azure/role-based-access-control/elevate-access-global-admin

Basic Tutorial: https://www.youtube.com/watch?v=AtAb_8Av4iU <br>
More In-Depth Tutorial: https://www.youtube.com/watch?v=Ma7VAQE7ga4 (Useful times: 9:19-20:23 && 22:59-27:42)<br><br>

# Billing

Using tags for billing/cost calculating:<br>

The API now supports cost management based on tags. "Today, filters support resource groups, instances and meters and with this release will also include tags. Scoping a budget to a tag or a set of tags will continue to leverage filters."<br>

<br>
Group by common properties to break down costs and identify top contributors. To group by resource tags, for example, select the tag key you want to group by. Costs are broken down by each tag value, with an extra segment for resources that don't have that tag applied.

<br>
<br>
Links:<br>
https://azure.microsoft.com/en-us/blog/announcing-the-support-for-tags-in-cost-management-apis/<br>
https://docs.microsoft.com/en-us/azure/cost-management-billing/costs/quick-acm-cost-analysis<br>

