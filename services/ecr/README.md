# Elastic Container Registry (ECR) on AWS

## Overview
- This is a Jinja templates for deploying Elastic Container Registry (ECR) on AWS with AWS CloudFormation.
- This AWS CloudFormation template is designed to create a Elastic Container Registry (ECR) stack to enables users to store, manage, and deploy Docker container images securely, making it easy to scale and deploy applications using containerization technology within AWS. This template is designed to be customizable with various parameters to adapt to different environments and use cases.

## Parameters
The template includes several parameters that allow you to customize the deployment:
1. **ECRRepoName**: Provide a concise name. A developer should be able to identify the repository contents by the name.
2. **Region**:  Provide a region.
3. **RepositoryImageTagMutability**:  Enable tag immutability to prevent image tags from being overwritten by subsequent image pushes using the same tag. Disable tag immutability to allow image tags to be overwritten.
4. **RepositoryType**:  Select the type of the ECR repo. Can be either a public or private one
5. **ScanRepo**: Enable scan on push to have each image automatically scanned after being pushed to a repository. If disabled, each image scan must be manually started to get scan results.
6. **ReadAccessARNs**: Select the appropriate users arn who can have read access to ecr repo
7. **ReadWriteAccessARNs**: Select the appropriate users arn who can have read and write access to ecr repo.
8. **ImageCount**: Number of most recent images to keep in the ECR repository.

## Conditions

Depending on the combination of parameter values, the template will create the appropriate record set with the specified properties.
- Below is the Condition variables defined in the template:
    - IsScanOnPushEnabled: This condition checks if the ScanRepo parameter is set to true. If true, it indicates that automatic image scanning should be enabled upon pushing images to the ECR repository. If false, manual scanning is required, and automatic scanning is disabled.

## Resources
- ECRPublicRepository 
    - Creates a public Elastic Container Registry (ECR) repository that allows public access to container images. Defines permissions for public access and enables image retrieval and management.
- ECRPrivateRepository 
    - Creates a private Elastic Container Registry (ECR) repository with customizable settings. Configures repository properties such as image tag mutability, image scanning, lifecycle policies, and access permissions based on IAM roles.

#### Jinja2 Templating
- Throughout the template, you can see Jinja2 syntax enclosed in double curly braces ({{ ... }}). These sections are placeholders for variables, and they likely get replaced with actual values when generating the CloudFormation template based on the context in which the Jinja template is processed.

#### Rendering CFT Template
- It's important to note that the actual values for the parameters and Jinja2 variables must be provided when creating a CloudFormation stack using this template. These values will determine the specific configuration of the stack.
- To use this template to create an AWS CloudFormation stack, you would typically process it through a Jinja2 renderer tool to replace the Jinja2 variables with their actual values, and then submit the resulting CloudFormation template to AWS for stack creation. The template is quite extensive and set up a ECR. The specific details of the infrastructure and its configuration would depend on the actual values provided for the parameters and Jinja2 variables.
- To render/parse the cloudofrmation jinja template to yaml use the below command
```
python3 render-templates.py <input_template_name>.j2 <variables_file_name>.yaml <output_cft_file_name>.yaml
```

## Usage
- From the above command the CFT template file(<output_cft_file_name>.yaml) will be generated, which can be used to create the AWS CFT stack.
