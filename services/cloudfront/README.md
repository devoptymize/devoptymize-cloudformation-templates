# CLOUDFRONT on AWS

## Overview
- This is a Jinja templates for deploying Cloudfront on AWS with AWS CloudFormation.
- This AWS CloudFormation template is designed to create a Cloudfront stack to to improve the performance, scalability, and availability of your web applications by distributing content globally and delivering it to users from the nearest edge location.

## Parameters
The template includes several parameters that allow you to customize the deployment:
1. **Environment**: The name of the environment (e.g., "dev," "prod").
2. **Distribution_type**: The type of the distribution i.e S3 or Loadbalancer
3. **cdn_name**:  The Name of the Cloudfront Distribution
4. **use_custom_domain**: Enable it to true to use CNAME for Cloudfront Distribution.
5. **origin_shield**: Origin Shield can help reduce the load on your origin.
6. **origin_path**: An optional path that CloudFront appends to the origin domain name when CloudFront requests content from the origin
7. **oac_name**: The comment for the CloudFront Origin Access Identity
8. **Price_class**: The price class for this distribution. One of PriceClass_All, PriceClass_200, PriceClass_100
9. **origin_protocol_policy**: Specifies the protocol (HTTP or HTTPS) that CloudFront uses to connect to the origin
10. **viewer_protocol_policy**: Specifies the protocol (HTTP or HTTPS) that CloudFront uses to connect to the origin
11. **allowed_http_methods**: controls which HTTP methods CloudFront processes and forwards to your Amazon S3 bucket or your custom origin
12. **compress**: Whether you want CloudFront to automatically compress certain files for this cache behavior. If so, specify true; if not, specify false
13. **ipv6**: If you want CloudFront to respond to IPv6 DNS requests with an IPv6 address for your distribution, specify true. If you specify false, CloudFront responds to IPv6 DNS requests with the DNS response code NOERROR and with no IP addresses.
14. **bucket_name**:The name of your S3 bucket (only needed for S3 distribution)
15. **loadbalancer_name**: The name of your load balancer (only needed for Load Balancer distribution)
16. **http_version**: The maximum HTTP version to support on the distribution. Allowed values are http1.1, http2, http2and3, and http3. The default is http2.
17. **default_root_object**: The object that you want CloudFront to request from your origin (for example, index.html)
18. **certificate_name**: ACM CERTIFICATE to secure HTTPS protocol
19. **aliases**: Extra CNAMEs (alternate domain names), if any, for this distribution
20. **webacl_name**: A unique identifier that specifies the AWS WAF web ACL, if any, to associate with this distribution.
21. **description**: A comment to describe the distribution. The comment cannot be longer than 128 characters.

## Conditions

- These conditions are used to control which type of Cloudfront (S3 or Loadbalancer) should be created on based the values of the DISTRIBUTION_TYPE and other parameters.
Depending on the combination of parameter values, the template will create the appropriate Cloudfront with the specified properties.
- Below is the Condition variables defined in the template:
    - UseCustomDomainCondition: This condition checks if it is enabled to "true". If it is, it evaluates to true, indicating that an alias should be used. If it is not set to "true", it evaluates to false.
    - IsS3Distribution: This condition checks if the Distribution_type is S3. If it is, it evaluates to true, indicating that a Cloudfront will be created based on S3 as origin domain.
    - IsLoadBalancerDistribution: This condition checks if the Distribution_type is Loadbalancer. If it is, it evaluates to true, indicating that a Cloudfront will be created based on Loadbalancer as origin domain.
    - UseACMCertificate: This condition checks if the ACMCertificateArn parameter is not equal to "". If it is, it evaluates to true, indicating that a SSL Certificate to be used.
    - UseCloudFrontDefaultCertificate: This condition checks if the ACMCertificateArn parameter is equal to "". If it is, it evaluates to true, indicating that a default Certificate to be used.

## Resources
- S3 bucket
    -  Creates a S3 bucket with configurable properties, such as the bucket name.
- CloudFront-Origin-Access-Control
    -  Creates a origin access control with configurable properties such as the name of the OAC.
- Cloudfront-Distribution
    -  Creates a Cloudfront Distribution with configurable properties, including dominname, Origin-access-control-id, Originpath, Originshield, Priceclass, defaultrootobject, Loggin-bucket, http-version, ipv6, targetoriginid, viewer_protocol_policy, compress, allowed_http_methods, viewer_certificate, aliases, comment, webaclid

#### Jinja2 Templating
- Throughout the template, you can see Jinja2 syntax enclosed in double curly braces ({{ ... }}). These sections are placeholders for variables, and they likely get replaced with actual values when generating the CloudFormation template based on the context in which the Jinja template is processed.

#### Rendering CFT Template
- It's important to note that the actual values for the parameters and Jinja2 variables must be provided when creating a CloudFormation stack using this template. These values will determine the specific configuration of the stack.
- To use this template to create an AWS CloudFormation stack, you would typically process it through a Jinja2 renderer tool to replace the Jinja2 variables with their actual values, and then submit the resulting CloudFormation template to AWS for stack creation. The template is quite extensive and set up a Cloudfront distribution. The specific details of the infrastructure and its configuration would depend on the actual values provided for the parameters and Jinja2 variables.
- To render/parse the cloudofrmation jinja template to yaml use the below command
```
python3 render-templates.py <input_template_name>.j2 <variables_file_name>.yaml <output_cft_file_name>.yaml
```

## Usage
- From the above command the CFT template file(<output_cft_file_name>.yaml) will be generated, which can be used to create the AWS CFT stack.
