# DevOptymize_CloudFormation_Templates

The DevOptymize_CloudFormation_Templates Repository hosts the collection of AWS CloudFormation templates in .j2 format, which can be used to provision individual resources and blueprints on AWS.

### Features
- Ready to use templates, helps in provisioning AWS resource and blueprints effortlessly.
- Re-usable.j2 template helps in keeping repetetive code snippets in loops and render it out into cloudformation templates dynamically based on the variables provided.
- Ready to use [render-template.py](./render-templates.py) file for ease of rendering the .j2 files.

- Blue prints
  - [Amazon VPC Configuration Guide](./services/aws-vpc-config)
  - [AWS DevOps pipeline architecture - CI/CD of Static-website (S3 CDN stack)](./services/aws-cicd-sw)
  - [AWS DevOps Pipeline architecture - CI/CD for Nodejs backend application](./services/aws-cicd-ms)

- Resources
  - [Network](./services/network)
  - [Key Pair](./services/key-pair)
  - [Security Group](./services/security-group)
  - [EC2](./services/ec2)
  - [Launch Template](./services/launch-template)
  - [ASG](./services/asg)
  - [Target Group](./services/lb-target-group)
  - [Load Balancer](./services/lb)
  - [RDS](./services/rds)
  - [Route53](./services/route-53)
  - [S3](./services/s3)
  - [ECR](./services/ecr)

### Pre-Requisites
Pre-requisites to be installed for rendering the templates:
- Make sure python3, jinja2, AWS-cli, jinja-cli is installed.
- Version details of the above mentioned packages are mentioned in the [render-template.py](./render-templates.py).

### Usage
Once you have the Jinja2 file and the Variable files ready here are the steps to create a stack.
- To render/parse the cloudformation jinja template to yaml use the below command
``` python3 render-templates.py <input_template_name>.j2 <variables_file_name>.yaml <output_cft_file_name>.yaml```
- Using the ```aws cloudformation create-stack --stack-name <stack name> --region <Region code> --template-body file://<output_cft_file_name.yaml>``` create the stack for the resource.
- To delete the cloudformation stack ```aws cloudformation delete-stack --stack-name <stack name> --region <Region code>```

### Contributing
We welcome contributions from the community to enhance the AWS CloudFormation template. If you would like to contribute, please follow our guidelines outlined in the [CONTRIBUTING.md](./CONTRIBUTING.md) file. You can submit feature requests, or pull requests to help us improve the template.

### License
