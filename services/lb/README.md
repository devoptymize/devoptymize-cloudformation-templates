# AWS LoadBalancer using CloudFormation template

## Overview
- This AWS CloudFormation template creates an Elastic Load Balancer (ELB) and associated resources based on the specified configuration parameters. - It supports both Application Load Balancer (ALB) and Network Load Balancer (NLB) types, providing flexibility in load balancing options.

## Parameters

1.**LoadBalancerName:**
  - *Type:* String
  - *Description:* The name of the ELB.
  - *Default:* "{{ loadbalancer_name }}"

2.**LoadBalancerType:**
  - *Type:* String
  - *Description:* The NLB or ALB.
  - *Default:* "{{ loadbalancer_type }}"
  - *Allowed Values:*
    - application
    - network

3.**Actions:**
  - *Type:* String
  - *Description:* Choose the action.
  - *Default:* "{{ action }}"

4.**LoadBalancerScheme:**
  - *Type:* String
  - *Description:* Select the scheme type.
  - *Default:* "{{ scheme }}"
  - *Allowed Values:*
    - internet-facing
    - internal

5.**IpAddressType:**
  - *Type:* String
  - *Description:* Select the IP address type.
  - *Default:* "{{ ip_address_type }}"
  - *Allowed Values:*
    - ipv4
    - dualstack

6.**Region:**
  - *Type:* String
  - *Description:* AWS region.
  - *Default:* "{{ region }}"

7.**Environment:**
  - *Type:* String
  - *Description:* AWS environment.
  - *Default:* "{{ environment }}"

8.**SecurityGroupId:**
  - *Type:* CommaDelimitedList
  - *Description:* The ID of the security group for the ELB.
  - *Default:* "{{ security_group_id }}"

9.**VpcId:**
  - *Type:* AWS::EC2::VPC::Id
  - *Description:* The ID of the VPC to deploy the ELB in.
  - *Default:* "{{ vpc_id }}"

10.**SubnetList:**
  - *Type:* List<AWS::EC2::Subnet::Id>
  - *Description:* Comma-separated list of subnet IDs.
  - *Default:* "{{ subnet_id }}"

11.**TargetGroupArn:**
  - *Type:* String
  - *Description:* ARN of the target group.
  - *Default:* "{{ target_group_arn }}"

12.**Port:**
  - *Type:* Number
  - *Description:* Mention the port number.
  - *Default:* {{ port }}

13.**Protocol:**
  - *Type:* String
  - *Description:* Select the protocol to use.
  - *Default:* "{{ protocol }}"
  - *Allowed Values:*
    - HTTP
    - HTTPS
    - TCP
    - UDP
    - TLS

14.**CertificateList:**
  - *Type:* String
  - *Description:* A list of SSL/TLS certificates.
  - *Default:* "{{ certificate_list }}"

15.**SecurityPolicy:**
  - *Type:* String
  - *Description:* The security policy for SSL/TLS connections.
  - *Default:* "{{ security_policy }}"

16.**ALPNPolicy:**
  - *Type:* CommaDelimitedList
  - *Description:* List of ALPN protocols for TLS connections.
  - *Default:* "{{alpn_policy}}"


## Conditions
- **UseApplicationLoadBalancer:** Checks if the load balancer type is "application" and the protocol is not "HTTPS."
- **ApplicationLoadbalancerHTTPS:** Checks if the load balancer type is "application" and the protocol is "HTTPS."
- **UseNetworkLoadBalancer:** Checks if the load balancer type is "network" and the protocol is not "TLS."
- **NetworkLoadBalancerTLS:** Checks if the load balancer type is "network" and the protocol is "TLS."

## Resources
- **LoadBalancer:** Creates the Elastic Load Balancer with specified properties.
- **ALBListener:** Creates an ALB listener when using an Application Load Balancer and the protocol is not "HTTPS."
- **ALBListenerHTTPS:** Creates an ALB listener when using an Application Load Balancer and the protocol is "HTTPS."
- **NLBListenerTLS:** Creates an NLB listener when using a Network Load Balancer and the protocol is "TLS."
- **NLBListener:** Creates an NLB listener when using a Network Load Balancer and the protocol is not "TLS."

## Rendering CFT Template
- It's important to note that the actual values for the parameters and Jinja2 variables must be provided when creating a CloudFormation stack using this template. These values will determine the specific configuration of the stack.
- To render/parse the CloudFormation jinja template to yaml use the below command
```
python3 render-templates.py <input_template_name>.j2 <variables_file_name>.yaml <output_cft_file_name>.yaml
```

## Usage
- From the above command the CFT template file(<output_cft_file_name>.yaml) will be generated, which can be used to create the stack for Target Group.

