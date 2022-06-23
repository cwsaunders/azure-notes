# azure-notes


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

1. 