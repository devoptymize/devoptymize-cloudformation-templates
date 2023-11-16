# Launch template provisioning on AWS

## Overview
- This is a Jinja templates for provisioning asg launch templates on AWS with AWS CloudFormation.
- This AWS CloudFormation template is designed to create a launch template stack to define our own custom launch configurations offering flexibility and control over your cloud infrastructure. This template is designed to be customizable with various parameters to adapt to different environments and use cases.

## Parameters
The template includes several parameters that allow you to customize the deployment:
1. **Region**: Region in which we need to create the launch template
2. **LaunchTemplateName**: Name of the launch template
3. **KeyPair**: Keypair name which needs to be used for spinning up the ec2 machines.
4. **InstanceType**: Instance type to be used for the ec2 machines
6. **SecurityGroupIds**: Ids of SGs which needs to be associated with the ec2 machines.
7. **IamInstanceProfile**: IAM instance profile name which needs to be attached to the ec2 machines.
8. **LinuxDeviceName**: Extra volume name for linux machines.
9. **WindowsDeviceName**: Extra volume name for windows machines.
10. **VolumeSizes**: Volume size in GB.
11. **OperatingSystem**: OS details whether windows or linux.
12. **AmiId**: AMI id which needs to be used for the ec2 machines.
13. **UserData**: User data, acts as the bootstrap script for the ec2 machines.

## Resources
- LaunchTemplate:
   -  Creates a launch templates with the details provided as parameters, custom userdata e.t.c.

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

