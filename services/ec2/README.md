# EC2 

## Overview
- This is a Jinja templates to create security group  on AWS with AWS CloudFormation.
- This AWS CloudFormation template is designed to create EC2 . This template is designed to be customizable with various parameters to adapt to different environments and use cases.

## Parameters
The template includes several parameters that allow you to customize the deployment:
1. **Keypairname**: KeypairName refers to a critical component in the secure access and authentication process of cloud instances.
2. **InstanceType**: InstanceType specifies the type of virtual machine or instance that is launched in a cloud computing environment. 
3. **AMIID**: AMIID stands for Amazon Machine Image ID. An AMI is a pre-configured template used to create virtual machines (EC2 instances) in Amazon Web Services (AWS).
4. **RootVolumeSize**:  RootVolumeSize indicates the size or capacity of the root volume attached to a virtual machine or instance. 
5. **ExtraVolumeSize**: ExtraVolumeSize refers to additional storage volumes that can be attached to a virtual machine or instance in a cloud environment.
6. **RootDeviceNameLin**: RootDeviceNameLin represents the name or identifier of the root device for Linux-based instances or virtual machines.
7. **RootDeviceNameWin**: RootDeviceNameWin is the equivalent of RootDeviceNameLin but for Windows-based instances or virtual machines. 
8. **WinDeviceNames**: WinDeviceNames refers to the device names or identifiers used for additional storage volumes attached to Windows-based instances in a cloud environment.
9. **LinDeviceNames**:  LinDeviceNames is similar to WinDeviceNames but applies to Linux-based instances
10. **SecurityGroupID**: SecurityGroupID represents a unique identifier for a security group in a cloud computing environment, such as AWS.
11. **OperatingSystem**: OperatingSystem refers to the software environment that runs on a virtual machine or instance in a cloud infrastructure. 
12. **InstanceName**:  InstanceName is a user-defined label or identifier given to a virtual machine or instance in a cloud environment. 
13. **SubnetId**: SubnetId refers to a unique identifier associated with a subnet within a virtual private cloud (VPC) in a cloud computing environment.

### Conditions
- These are conditionals that can be used to control resource creation within the CloudFormation template. They are based on the values of certain parameters or resource attributes.
  - IsWindows: This condition is used to check if the value of the OperatingSystem parameter is equal to "windows." It is defined as `IsWindows: !Equals [!Ref OperatingSystem, windows]` This condition will evaluate to true if the value of the OperatingSystem parameter is "windows," and false otherwise.
  - IsAdditional: This condition is used to check if the value of the AdditionalVolume parameter is equal to "yes." It is defined as follows:
  `IsAdditional: !Equals [!Ref AdditionalVolume, yes]`. This condition will evaluate to true if the value of the AdditionalVolume parameter is "yes," and false otherwise.

#### Jinja2 Templating
- Throughout the template, you can see Jinja2 syntax enclosed in double curly braces ({{ ... }}). These sections are placeholders for variables, and they likely get replaced with actual values when generating the CloudFormation template based on the context in which the Jinja template is processed.

## Resources

1. AWS EC2 Instance (LinuxInstance): 
   - Type: 'AWS::EC2::Instance' 
   - Properties: ImageId: The ID of the Amazon Machine Image (AMI) to use for the instance (referenced from AMIID parameter).
   - InstanceType: The EC2 instance type (referenced from InstanceType parameter).
   - SubnetId: The ID of the VPC Subnet in which the instance will be launched (referenced from SubnetId parameter).
   - SecurityGroupIds: A list of security group IDs to attach to the EC2 instance (split from SecurityGroupID parameter).
   - KeyName: The EC2 KeyPair name to enable SSH access to the instance (referenced from KeyName parameter).
   
2. Tags:
   - A tag is applied to the EC2 instance with a key of "Name" and the value is set to the InstanceName parameter.

#### Rendering CFT Template
- It's important to note that the actual values for the parameters and Jinja2 variables must be provided when creating a CloudFormation stack using this template. These values will determine the specific configuration of the stack.
- To use this template to create an AWS CloudFormation stack, you would typically process it through a Jinja2 renderer tool to replace the Jinja2 variables with their actual values, and then submit the resulting CloudFormation template to AWS for stack creation. The template is quite extensive and create EC2 The specific details of the infrastructure and its configuration would depend on the actual values provided for the parameters and Jinja2 variables.
- To render/parse the cloudofrmation jinja template to yaml use the below command
```
python3 render-templates.py <input_template_name>.j2 <variables_file_name>.yaml <output_cft_file_name>.yaml
```

## Usage
- From the above command the CFT template file(<output_cft_file_name>.yaml) will be generated, which can be used to create the AWS CFT stack.
