# SECURITY GROUP

## Overview
- This is a Jinja templates to create security group  on AWS with AWS CloudFormation.
- This AWS CloudFormation template is designed to create security group . This template is designed to be customizable with various parameters to adapt to different environments and use cases.

## Parameters
The template includes several parameters that allow you to customize the deployment:
1. **SecurityGroupName**:  This parameter refers to the name assigned to a security group within a cloud networking environment.
2. **SecurityGroupDescription**: This parameter provides a textual description or label for a security group.
3. **VpcId**: The VpcId parameter stands for "Virtual Private Cloud Identifier." It refers to a unique identifier associated with a virtual private cloud (VPC) in a cloud infrastructure.
4. **Region**: The Region parameter indicates the geographical region or data center location within a cloud provider's infrastructure where the resources and services are hosted.
5. **IngressRules**: Ingress rules are a set of rules that define the inbound traffic access permissions for a security group. They specify what types of incoming traffic are allowed or denied to resources associated with the security group.

#### Jinja2 Templating
- Throughout the template, you can see Jinja2 syntax enclosed in double curly braces ({{ ... }}). These sections are placeholders for variables, and they likely get replaced with actual values when generating the CloudFormation template based on the context in which the Jinja template is processed.

#### Rendering CFT Template
- It's important to note that the actual values for the parameters and Jinja2 variables must be provided when creating a CloudFormation stack using this template. These values will determine the specific configuration of the stack.
- To use this template to create an AWS CloudFormation stack, you would typically process it through a Jinja2 renderer tool to replace the Jinja2 variables with their actual values, and then submit the resulting CloudFormation template to AWS for stack creation. The template is quite extensive and create securitygroup The specific details of the infrastructure and its configuration would depend on the actual values provided for the parameters and Jinja2 variables.
- To render/parse the cloudofrmation jinja template to yaml use the below command
```
python3 render-templates.py <input_template_name>.j2 <variables_file_name>.yaml <output_cft_file_name>.yaml
```

## Usage
- From the above command the CFT template file(<output_cft_file_name>.yaml) will be generated, which can be used to create the AWS CFT stack.
