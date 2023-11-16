# ASG Configuration on AWS

## Overview
- This is a Jinja templates for deploying Autoscaling group on AWS with AWS CloudFormation.
- This AWS CloudFormation template is designed to create a ASG stack, offering flexibility and control over your cloud infrastructure. This template is designed to be customizable with various parameters to adapt to different environments and use cases.

## Parameters
The template includes several parameters that allow you to customize the deployment:
1. **Region**: AWS region in which we need to provision the ASG.
2. **AutoScalingGroupName**: Name for the ASG which needs to be provisioned.
3. **SubnetId**: Id of subnet in which we need to provision the ASG.
4. **MaximumSize**: Maximum limit of the ASG scaling.(expected in numbers)
5. **MinimumSize**: Minimum limit of ASG scaling.(expected in numbers)
6. **DesiredCapacity**: Desired capacity of the ASG scaling. (expected in numbers)
7. **LaunchTemplateName**: Name of launch template which should be used for creating the ASG.
8. **LaunchTemplateVersion**: Version of launch template to be used.
9. **LoadBalancer**: Name of the load balancer to which the ASG should be associated with.
10. **SnsTopic**: ARN of the sns topic to which the autoscaling notifications to be send. 

## Resources
- Auto Scaling Group:
   -  Provisions an autoscaling group into AWS in the vpc and subnet of our choice with custom launch template opted by us.
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

