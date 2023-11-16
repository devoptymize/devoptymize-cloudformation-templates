# AWS Target Group using CloudFormation template

## Overview
This AWS CloudFormation template is designed to create a target group for an Application Load Balancer (ALB) or other AWS resources based on the specified target type. The template utilizes Jinja syntax for parameter defaults and conditions to provide dynamic configurations.

## parameters
1.**TargetGroupName**:
   - Type: String
   - Description: Name of the target group.
   - Default: "{{ target_group_name }}"

2.**PortNumber**:
   - Type: Number
   - Description: Port number for the target group.
   - Default: "{{ port_number }}"If target_type is 'lambda', default: '0' Otherwise, default: "{{ port_number }}"

3.**TargetType**:
   - Type: String
   - Description: Type of the target (instance, IP, Lambda, etc.).
   - Default: "{{ target_type }}"

4.**Protocol**:
   - Type: String
   - Description: Protocol type for the target group.
   - Default: "{{ protocol_type }}"

5.**VpcId**:
   - Type: String
   - Description: ID of the VPC.
   - Default: "{{ vpc_id }}"

6.**Region**:
   - Type: String
   - Description: Region for the target group attachment.
   - Default: "{{ region }}"

7.**IpAddress**:
   - Type: CommaDelimitedList
   - Description: IP address for the target group attachment.
   - Default: "{{ ip_address }}"

8.**ApplicationLoadBalancer**:
   - Type: String
   - Description: Application Load Balancer for the target group attachment.
   - Default: "{{ application_load_balancer }}"

9.**InstanceName**:
   - Type: String
   - Description: Name of the instance for the target group attachment.
   - Default: "{{ instance_name }}"
    
10.**LambdaFunctionName**:
   - Type: String
   - Description: Name of the Lambda function.
   - Default: "{{ lambda_function_name }}"

## Conditions
1.**IsInstanceTarget**:
   - Checks if the target type is "instance."

2.**IsIpTarget**:
   - Checks if the target type is "IP."

3.**IsLambdaTarget**:
   - Checks if the target type is "Lambda."

4.**IsAlbTarget**:
   - Checks if the target type is "ALB."


## Resources

### Type: AWS::ElasticLoadBalancingV2::TargetGroup
- Creates an AWS Elastic Load Balancing V2 Target Group based on the target type condition.
- Customizes properties such as Port, Protocol, VpcId, and Targets based on the target type.

### Type: AWS::Lambda::Permission
- Creates an AWS Lambda permission to invoke the function if the target type is Lambda.


## Rendering CFT Template
- It's important to note that the actual values for the parameters and Jinja2 variables must be provided when creating a CloudFormation stack using this template. These values will determine the specific configuration of the stack.
- To render/parse the CloudFormation jinja template to yaml use the below command
```
python3 render-templates.py <input_template_name>.j2 <variables_file_name>.yaml <output_cft_file_name>.yaml
```

## Usage
- From the above command the CFT template file(<output_cft_file_name>.yaml) will be generated, which can be used to create the stack for Target Group.


