# S3 on AWS

## Overview
- This is a Jinja templates for deploying S3 on AWS with AWS CloudFormation.
- This AWS CloudFormation template is designed to create a S3 which allows individuals and businesses to store and retrieve data, such as documents, images, videos, and backups, securely and durably in the cloud. S3 offers features like high scalability, data redundancy, versioning, and fine-grained access controls, making it suitable for a wide range of applications, from data archiving to hosting static websites and powering data analytics pipelines.

## Parameters
The template includes several parameters that allow you to customize the deployment:
1. **Environment**: The name of the environment (e.g., "dev," "prod").
2. **BUCKETNAME**: It is a globally unique string that helps you organize and access your data within Amazon S3. Bucket names must be lowercase and can contain letters, numbers, hyphens, and periods. 
3. **BUCKET_KEY_ENABLED**: It is a feature in Amazon S3 that allows you to execute custom code on data retrieved from S3 before it is returned to the requester. This enables you to perform data transformations, filtering, or other operations on the data within an S3 bucket.
4. **BUCKET_POLICY**: A bucket policy is a set of rules or permissions that you can configure for an Amazon S3 bucket. It defines who can access the data within the bucket and what actions they can perform.

## Resources
- S3 bucket
- Bucket Policy
    
#### Jinja2 Templating
- Throughout the template, you can see Jinja2 syntax enclosed in double curly braces ({{ ... }}). These sections are placeholders for variables, and they likely get replaced with actual values when generating the CloudFormation template based on the context in which the Jinja template is processed.

#### Rendering CFT Template
- It's important to note that the actual values for the parameters and Jinja2 variables must be provided when creating a CloudFormation stack using this template. These values will determine the specific configuration of the stack.
- To use this template to create an AWS CloudFormation stack, you would typically process it through a Jinja2 renderer tool to replace the Jinja2 variables with their actual values, and then submit the resulting CloudFormation template to AWS for stack creation. The template is quite extensive and set up a S3. The specific details of the infrastructure and its configuration would depend on the actual values provided for the parameters and Jinja2 variables.
- To render/parse the cloudofrmation jinja template to yaml use the below command
```
python3 render-templates.py <input_template_name>.j2 <variables_file_name>.yaml <output_cft_file_name>.yaml
```

## Usage
- From the above command the CFT template file(<output_cft_file_name>.yaml) will be generated, which can be used to create the AWS CFT stack.
