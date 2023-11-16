# RDS CLUSTER

## Overview
-  This is a Jinja templates for deploying RDS cluster on AWS with AWS CloudFormation.

## Parameters 
The template includes several parameters that allow you to customize the deployment:
1. **RdsClusterIdentifier**:  This is the unique identifier for an Amazon RDS (Relational Database Service) cluster. It is used to distinguish one RDS cluster from another.
2. **EngineType**: EngineType refers to the database engine that the RDS cluster uses, such as MySQL, PostgreSQL, Oracle, or SQL Server.
3. **EngineVersion**: EngineVersion specifies the version of the database engine software that the RDS cluster runs. For example, MySQL 5.7 or PostgreSQL 12.
4. **DbMasterUsername**: This is the username of the master database user who has superuser privileges and can perform administrative tasks within the RDS cluster.
5. **DbMasterPassword**: DbMasterPassword is the password associated with the master database user. It is used for authentication when connecting to the RDS cluster.
6. **DbInstanceClass**: DbInstanceClass determines the compute and memory capacity allocated to each individual database instance within the RDS cluster. It comes in various sizes, such as db.t2.micro, db.m4.large, etc.
7. **VpcName**: VpcName represents the name of the Virtual Private Cloud (VPC) in which the RDS cluster is deployed. A VPC is a logically isolated section of the AWS cloud where you can launch AWS resources.
8. **VpcId**: VpcId is the unique identifier for the VPC in which the RDS cluster resides.
9. **SubnetGroup**: A subnet group is a collection of subnets within the VPC where the RDS instances can be placed. It defines the network configuration for the RDS cluster.
10. **SubnetName**: SubnetName is the name associated with a specific subnet within the subnet group.
11. **SubnetId**: SubnetId is the unique identifier for a specific subnet within the subnet group.
12. **SecurityGroupName**: SecurityGroupName is the name of a security group, which acts as a virtual firewall for controlling inbound and outbound traffic to the RDS cluster instances.
13. **SecurityGroupId**: SecurityGroupId is the unique identifier for the security group associated with the RDS cluster.
14. **PublicAccess**: PublicAccess determines whether the RDS cluster is accessible from the public internet. It can be set to "true" or "false."
15. **DbInstanceOne**: This may refer to the first individual database instance within the RDS cluster.
16. **DbInstanceOneCustom**: It likely indicates custom configuration or settings specific to the first database instance.
17. **DbInstanceTwo**: This may refer to the second individual database instance within the RDS cluster.
18. **DbInstanceTwoCustom**:  It likely indicates custom configuration or settings specific to the second database instance.
19. **DbInstanceThree**: This may refer to the third individual database instance within the RDS cluster.
20. **DbInstanceThreeCustom**: It likely indicates custom configuration or settings specific to the third database instance.
21. **DbClusterInstanceClass**: DbClusterInstanceClass specifies the compute and memory capacity for instances in an Aurora RDS cluster.
22. **RdsStorage**: RdsStorage refers to the amount of storage allocated for the RDS cluster.
23. **StorageType**: StorageType defines the type of storage used by the RDS cluster, such as General Purpose (SSD), Provisioned IOPS (SSD), or Magnetic.
24. **Iops**: Iops (Input/Output Operations Per Second) is the provisioned IOPS for storage when using Provisioned IOPS storage type.
25. **Encryption**: Encryption determines whether data at rest in the RDS cluster is encrypted for security purposes.
26. **ParameterGroup**: ParameterGroup is a set of database engine parameter values that can be applied to configure and tune the RDS cluster.
27. **ParameterGroupNew**: This might indicate a new set of parameter values for configuring the RDS cluster.
28. **ClusterParameterGroup**: ClusterParameterGroup is similar to ParameterGroup but applies to Aurora RDS clusters.
29. **ClusterParameterGroupNew**: This likely indicates a new set of parameter values for configuring Aurora RDS clusters.
30. **EnableStorageAutoscaling**: This option allows automatic scaling of storage capacity based on the workload and storage needs of the RDS cluster.
31. **EnableCloudwatchLogsExports**: It specifies which types of logs (e.g., error logs, slow query logs) are exported to Amazon CloudWatch for monitoring and analysis.
32. **DbParameterFamily**: DbParameterFamily categorizes database engine parameters into families based on their functionality and purpose. 

## Conditions
- These are conditionals that can be used to control resource creation within the CloudFormation template. They are based on the values of certain parameters or resource attributes.
   - ShouldAllocateStorage: This condition checks if the EngineType parameter is either "mysql" or "postgres".
   - ShouldAllocateIops: This condition checks if the EngineType parameter is not "aurora-mysql" or "aurora-postgresql".
   - ShouldAllocateDbClusterInstanceClass:  It determines whether the DB cluster instance class should be specified based on the selected database engine type.
   - ShouldAllocateStorageType:  It determines whether the storage type for the RDS cluster should be specified based on the selected database engine type.
   - ShouldUseDbParameterGroup: It determines whether a DB parameter group should be specified based on the selected database engine type.
   - ShouldUseSubnetName:  It determines whether a DB subnet group should be created based on the presence of a subnet name.
   - IsNullDbParameterGroup: It determines whether the DB parameter group should be created or not.
   - IsNullClusterParameterGroup: It determines whether the cluster parameter group should be created or not.
   - IsNullSubnetGroup: It determines whether the DB subnet group should be specified based on the selected database engine type.
   - ShouldEnablePublicAccess: It determines whether the RDS cluster should be publicly accessible. This condition is based on the engine_type parameter being "mysql" or "postgres".
   - IsMySQLOrAuroraMySQL: It is used to conditionally set properties for MySQL and Aurora MySQL.
   - EnableStorageAutoscalingCondition: It determines whether storage auto-scaling properties should be specified based on the selected database engine type and the value of EnableStorageAutoscaling.
   - ShouldUseCloudWatchLogs:  It determines whether CloudWatch logs should be enabled for the RDS cluster.
   - IsAuroraPostgreSQL, IsPostgreSQL, IsMySQL, IsAuroraMySQL, IsAurora: These conditions check the selected database engine type and are used to set properties and conditions specific to each engine type.

## Resources
1. DB Subnet Group (DbSubnetGroup): 
   - Type: AWS::RDS::DBSubnetGroup
   - Type: AWS::RDS::DBSubnetGroup
2. RDS Cluster (RdsCluster):
   - Type: AWS::RDS::DBCluster
   - Properties: Various properties based on the input parameters and conditions, such as engine type, version, cluster identifier, master username and password, security group, availability zones, backup settings, and more.
3. RDS Cluster Instance One (RdsClusterInstanceOne):
   - Type: AWS::RDS::DBInstance
   - Condition: IsAurora
   - Properties: Properties for the first RDS instance in the Aurora cluster, including engine type, parameter group, instance identifier, instance class, and more.
4. RDS Cluster Instance Two (RdsClusterInstanceTwo):
   - RDS Cluster Instance Two (RdsClusterInstanceTwo)
   - Condition: IsAurora
   - Properties: Properties for the second RDS instance in the Aurora cluster, similar to Instance One.
5. RDS Cluster Instance Three (RdsClusterInstanceThree):
   - Type: AWS::RDS::DBInstance
   - Condition: IsAurora
   - Properties: Properties for the third RDS instance in the Aurora cluster, similar to Instance One.
6. Security Group Ingress Rule (RdsClusterSecurityGroupIngress):
   - Type: AWS::EC2::SecurityGroupIngress
   - Condition: ShouldEnablePublicAccess
   - Properties: Specifies the IP protocol (TCP), port range (based on engine type), and CIDR IP range for public access.

## Jinja2 Templating
- Throughout the template, you can see Jinja2 syntax enclosed in double curly braces ({{ ... }}). These sections are placeholders for variables, and they likely get replaced with actual values when generating the CloudFormation template based on the context in which the Jinja template is processed.
## Rendering CFT Template
- It's important to note that the actual values for the parameters and Jinja2 variables must be provided when creating a CloudFormation stack using this template. These values will determine the specific configuration of the stack.
- To use this template to create an AWS CloudFormation stack, you would typically process it through a Jinja2 renderer tool to replace the Jinja2 variables with their actual values, and then submit the resulting CloudFormation template to AWS for stack creation. The specific details of the infrastructure and its configuration would depend on the actual values provided for the parameters and Jinja2 variables.
- To render/parse the cloudofrmation jinja template to yaml use the below command
```
python3 render-templates.py <input_template_name>.j2 <variables_file_name>.yaml <output_cft_file_name>.yaml
```
## Usage
- From the above command the CFT template file(<output_cft_file_name>.yaml) will be generated, which can be used to create the stack AWS CFT.
