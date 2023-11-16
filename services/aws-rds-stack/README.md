## Amazon RDS on AWS

## Overview
- This is a Jinja templates for deploying WordPress on AWS using AWS Virtual Private Cloud (VPC), security groups, Auto Scaling Groups (ASG),Amazon EC2 (Elastic Cloud Compute), Amazon RDS (Relational Database Service), AWS Cloudwatch, AWS KMS (Key Management Service), and AWS SNS (Simple Notification Service) with AWS CloudFormation.
- This AWS CloudFormation template is designed to create a Amazon RDS on AWS stack for hosting a WordPress application. The stack consists of multiple components, including AWS Virtual Private Cloud (VPC), security groups, Auto Scaling Groups (ASG),Amazon EC2 (Elastic Cloud Compute), Amazon RDS (Relational Database Service), AWS Cloudwatch, AWS KMS (Key Management Service), and AWS SNS (Simple Notification Service). This template is designed to be customizable with various parameters to adapt to different environments and use cases.

## Parameters
The template includes several parameters that allow you to customize the deployment:
1. **Env**: The name of the environment (e.g., "dev," "prod").
2. **StackName**: The name of the CloudFormation stack to create.
- Network Configuration
3. **VPCCIDR**: The CIDR range for your Virtual Private Cloud (VPC).
4. **PublicSubnetCIDRs**: A list of public subnet CIDR blocks inside the VPC.
5. **PrivateSubnetCIDRs**: A list of private subnet CIDR blocks inside the VPC.
- Launch Template 
6. **KeyPair**: The name of the Key Pair to use for EC2 instances.
7. **InstanceType**: The type of EC2 instances to launch.
8. **AmiId**: The ID of the Amazon Machine Image (AMI) to use for EC2 instances.
9. **VolumeSizes**: Volume sizes to be attached to the launch template.
10. **VolumeType**: Volume types to be attached to the launch template.
- ASG Configuration
11. **MinimumSize**: The minimum number of instances in the Auto Scaling group.
12. **MaximumSize**: The maximum number of instances in the Auto Scaling group.
13. **DesiredCapacity**: The desired capacity of the Auto Scaling group.
- Amazon RDS Cluster Configuration
14. **RdsIdentifier**: The name of the Amazon RDS DB cluster.
15. **EngineType**: Choose the database engine type.
16. **EngineVersion**: Choose the database engine version.
17. **DbMasterUsername**: DB master username.
18. **DbMasterPassword**: DB master password (not echoed).
19. **DbInstanceClass**: DB instance class.
20. **RdsStorage**: The storage value of the rds.
21. **LogExports**: Enable log exports to CloudWatch (Yes or No).
- SNS Notification
22. **Endpoint**: Email address to receive notifications via SNS.

## Conditions
- These are conditionals that can be used to control resource creation within the CloudFormation template. They are based on the values of certain parameters or resource attributes. For example, there are conditions like IsMySQL, IsPostgreSQL, etc., that determine whether specific resources should be created based on user-provided values.
- Below is the Condition variables defined in the template:
    - IsMySQL: This condition checks if the value of the "EngineType" parameter is equal to "mysql." If true, it implies that the database engine being used is MySQL, and specific configurations or resources related to MySQL can be conditionally defined in the CloudFormation template.
    - IsPostgreSQL: This condition checks if the value of the "EngineType" parameter is equal to "postgres." If true, it implies that the database engine being used is PostgreSQL, and specific configurations or resources related to PostgreSQL can be conditionally defined in the CloudFormation template.
    - IsLogExportEnabled: This condition checks whether the value of the "LogExports" parameter is equal to 'yes'. If true, it signifies that log exporting is enabled, allowing you to conditionally define resources or configurations related to log export functionality in your CloudFormation template.

## Resources
- VPC Creation
    - Creates a Virtual Private Cloud (VPC) with specified CIDR blocks and necessary configurations.
- Internet Gateway
    - Creates an Internet Gateway and attaches it to the VPC for public internet access.
- Public Subnets
    - Creates public subnets and associates them with a public route table.
- Private Subnets
    - Creates private subnets and associates them with a private route table.
- IAM Roles and Instance Profiles:
    - Creates IAM roles and instance profile for the instances.
- Launch template and Auto Scaling Groups
    - Defines Launch template and Auto Scaling groups for public and private instances.
- RDS Instances
    - Creates DB instances and associates them with a subnet group.
- SNS Topic
    - Creates the SNS notifications for the RDS Instances.
## Jinja2 Templating
- Throughout the template, you can see Jinja2 syntax enclosed in double curly braces ({{ ... }}). These sections are placeholders for variables, and they likely get replaced with actual values when generating the CloudFormation template based on the context in which the Jinja template is processed.
## Rendering CFT Template
- It's important to note that the actual values for the parameters and Jinja2 variables must be provided when creating a CloudFormation stack using this template. These values will determine the specific configuration of the stack.
- To use this template to create an AWS CloudFormation stack, you would typically process it through a Jinja2 renderer tool to replace the Jinja2 variables with their actual values, and then submit the resulting CloudFormation template to AWS for stack creation. The template is quite extensive and set up a multi-tier infrastructure stack for hosting WordPress, including VPC, subnets, security groups, RDS clusters, Elasticache clusters, a CloudFront distribution, and more. The specific details of the infrastructure and its configuration would depend on the actual values provided for the parameters and Jinja2 variables.
- To render/parse the cloudofrmation jinja template to yaml use the below command
```
python3 render-templates.py <input_template_name>.j2 <variables_file_name>.yaml <output_cft_file_name>.yaml
```
## Usage
- From the above command the CFT template file(<output_cft_file_name>.yaml) will be generated, which can be used to create the stack AWS CFT.


