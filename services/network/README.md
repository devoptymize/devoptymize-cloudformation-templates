# Network Configuration on AWS

## Overview
- This is a Jinja templates for deploying Network Configuration on AWS with AWS CloudFormation.
- This AWS CloudFormation template is designed to create a Network Configuration stack to define your own IP address range, subnets, routing, security, and network connectivity options, offering flexibility and control over your cloud infrastructure. This template is designed to be customizable with various parameters to adapt to different environments and use cases.

## Parameters
The template includes several parameters that allow you to customize the deployment:
1. **VPCCIDR**: The primary IPv4 address range for your Amazon VPC, defining the range of IP addresses available for your virtual private cloud.
2. **PublicSubnetCIDRs**: The IPv4 address ranges assigned to public subnets within your VPC, typically associated with resources that require direct internet access.
3. **PrivateSubnetCIDRs**:  The IPv4 address ranges assigned to private subnets within your VPC, typically used for resources that should not have direct internet connectivity.
4. **VPCName**: The user-defined name or label for your Amazon VPC, providing a human-readable identifier for the VPC in your AWS environment.

## Resources
- VPC:
   -  Defines an Amazon Virtual Private Cloud (VPC) with a specified CIDR block and enables DNS support and DNS hostnames. Tags the VPC with a user-defined name.
- InternetGateway:
   - Creates an Internet Gateway for the VPC to provide internet access. It is tagged with a name based on the AWS Stack Name.
- InternetGatewayAttachment:
   - Attaches the Internet Gateway to the VPC, allowing traffic to flow between the VPC and the internet.
- PublicSubnet:
   - Defines a public subnet within the VPC with a specified CIDR block and associates it with an availability zone. Tags the subnet with a user-defined name.
- PublicRouteTable:
   - Creates a route table for a public subnet within the VPC and tags it with a user-defined name.
- PublicRoute:
   - Defines a route in the public route table to allow internet traffic through the Internet Gateway.
- PublicRouteTableAssociation:
   - Associates the public route table with the respective public subnet.
- NatEIP:
   - Allocates an Elastic IP (EIP) address for use with Network Address Translation (NAT) Gateway. Tagged with a user-defined name.
- NatGateway:
   - Creates a NAT Gateway in the first public subnet. Associates it with the allocated EIP and tags it with a user-defined name.
- PrivateSubnet:
   - Defines a private subnet within the VPC with a specified CIDR block and associates it with an availability zone. Tags the subnet with a user-defined name.
- PrivateRouteTable:
   - Creates a route table for a private subnet within the VPC and tags it with a user-defined name.
- PrivateRoute:
   - Defines a route in the private route table to route traffic through the NAT Gateway.
- PrivateRouteTableAssociation:
   - Associates the private route table with the respective private subnet.

#### Jinja2 Templating
- Throughout the template, you can see Jinja2 syntax enclosed in double curly braces ({{ ... }}). These sections are placeholders for variables, and they likely get replaced with actual values when generating the CloudFormation template based on the context in which the Jinja template is processed.

#### Rendering CFT Template
- It's important to note that the actual values for the parameters and Jinja2 variables must be provided when creating a CloudFormation stack using this template. These values will determine the specific configuration of the stack.
- To use this template to create an AWS CloudFormation stack, you would typically process it through a Jinja2 renderer tool to replace the Jinja2 variables with their actual values, and then submit the resulting CloudFormation template to AWS for stack creation. The template is quite extensive and set up a network configuration. The specific details of the infrastructure and its configuration would depend on the actual values provided for the parameters and Jinja2 variables.
- To render/parse the cloudofrmation jinja template to yaml use the below command
```
python3 render-templates.py <input_template_name>.j2 <variables_file_name>.yaml <output_cft_file_name>.yaml
```

## Usage
- From the above command the CFT template file(<output_cft_file_name>.yaml) will be generated, which can be used to create the AWS CFT stack.

