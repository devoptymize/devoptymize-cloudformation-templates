# Hosted-zone on AWS

## Overview
- This is a Jinja templates for deploying Hosted-zone on AWS with AWS CloudFormation.
- This AWS CloudFormation template is designed to create a Route53 stack to manage the DNS for your domain names and ensure the availability and performance of your applications and resources. This template is designed to be customizable with various parameters to adapt to different environments and use cases.

## Parameters
The template includes several parameters that allow you to customize the deployment:
1. **Environment**: The name of the environment (e.g., "dev," "prod").
2. **HOSTEDZONENAME**: The name for the hosted zone. For example, cloudifyops.com
3. **HOSTED_ZONE_TYPE**: The type of the hostedzone. It can either be public or private.
4. **ROUTE53_VPCNAME**: The VPCs to associate with the hosted zone. Options are dynamically populated based on other parameters.

## Conditions
1. **if route53_vpcid**: This condition checks if the route53_vpcid is empty. If it's empty, Public hosted zone will be created. Otherwise a Private hosted zone will be created.

## Resources
- Hosted-zone
    -  Creates a hosted-zone with configurable properties, including vpc-id, vpc-region, Name.
#### Jinja2 Templating
- Throughout the template, you can see Jinja2 syntax enclosed in double curly braces ({{ ... }}). These sections are placeholders for variables, and they likely get replaced with actual values when generating the CloudFormation template based on the context in which the Jinja template is processed.

#### Rendering CFT Template
- It's important to note that the actual values for the parameters and Jinja2 variables must be provided when creating a CloudFormation stack using this template. These values will determine the specific configuration of the stack.
- To use this template to create an AWS CloudFormation stack, you would typically process it through a Jinja2 renderer tool to replace the Jinja2 variables with their actual values, and then submit the resulting CloudFormation template to AWS for stack creation. The template is quite extensive and set up a Route53. The specific details of the infrastructure and its configuration would depend on the actual values provided for the parameters and Jinja2 variables.
- To render/parse the cloudofrmation jinja template to yaml use the below command
```
python3 render-templates.py <input_template_name>.j2 <variables_file_name>.yaml <output_cft_file_name>.yaml
```

## Usage
- From the above command the CFT template file(<output_cft_file_name>.yaml) will be generated, which can be used to create the AWS CFT stack.
