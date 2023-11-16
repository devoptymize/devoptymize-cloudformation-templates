# Elastic Kubernetes Service (EKS) on AWS

## Overview
- This is a Jinja templates for deploying Elastic Kubernetes Service (EKS) on AWS with AWS CloudFormation.
- This AWS CloudFormation template is designed to create a Elastic Kubernetes Service (EKS) stack to provides a highly available and secure platform to run, manage, and scale containerized workloads with ease. This template is designed to be customizable with various parameters to adapt to different environments and use cases.

## Parameters
The template includes several parameters that allow you to customize the deployment:
1. **Env**: The name of the environment (e.g., "dev," "prod").
2. **ClusterName**: The name of the Cluster to create.
3. **ClusterVersion**:  Version of the EKS cluster
4. **logtypes**: 
5. **EndpointPrivateAccess**: Specify whether to enable private access to the EKS cluster endpoint (true/false)
6. **VpcId**: VPC where the EKS cluster will be created
7. **SubnetId**: Subnets where the EKS cluster will be created.
8. **NodeGroupName**: Name of the node group  .
9. **NodeGroupMaxSize**: Maximum number of nodes in the node group.
10. **NodeGroupMinSize**:Minimum number of nodes in the node group.
11. **NodeInstanceType**: EC2 instance type for the nodes
12. **VolumeSize**: Size of the worker node EBS volume in GB
13. **VolumeType**: Type of the worker node EBS volume

## Resources
- EC2 Security Group
    - Creates a custom EC2 security group for the EKS cluster with defined inbound and outbound rules. Allows communication between nodes, pods, and cluster API server while restricting unnecessary access.
- EKS Cluster
    - Deploys an Amazon Elastic Kubernetes Service (EKS) cluster with specified configurations like logging, VPC access, and security groups. Enables cluster-level logging for selected log types and associates the custom security group for network access.
- EKS Nodegroup
    - Establishes a node group within the EKS cluster with defined properties, such as capacity, scaling, and instance types.Utilizes the specified IAM role for worker nodes and connects them to the cluster's subnets.
- IAM Role (ClusterRole)
    - Creates an IAM role for the EKS cluster to allow communication and management of AWS resources. Grants permissions for EKS cluster actions and associated policies for cluster services.
- IAM Role (NodeInstanceRole)
    - Defines an IAM role for EKS worker nodes, allowing them to interact with EKS and other AWS services. Attaches policies for worker node permissions, network interfaces, and container registry read-only access.

#### Jinja2 Templating
- Throughout the template, you can see Jinja2 syntax enclosed in double curly braces ({{ ... }}). These sections are placeholders for variables, and they likely get replaced with actual values when generating the CloudFormation template based on the context in which the Jinja template is processed.

#### Rendering CFT Template
- It's important to note that the actual values for the parameters and Jinja2 variables must be provided when creating a CloudFormation stack using this template. These values will determine the specific configuration of the stack.
- To use this template to create an AWS CloudFormation stack, you would typically process it through a Jinja2 renderer tool to replace the Jinja2 variables with their actual values, and then submit the resulting CloudFormation template to AWS for stack creation. The template is quite extensive and set up a EKS. The specific details of the infrastructure and its configuration would depend on the actual values provided for the parameters and Jinja2 variables.
- To render/parse the cloudofrmation jinja template to yaml use the below command
```
python3 render-templates.py <input_template_name>.j2 <variables_file_name>.yaml <output_cft_file_name>.yaml
```

## Usage
- From the above command the CFT template file(<output_cft_file_name>.yaml) will be generated, which can be used to create the AWS CFT stack.


