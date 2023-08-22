# DevOptymize_CloudFormation_Templates

The DevOptymize_CloudFormation_Templates Repository is a version-controlled collection of AWS CloudFormation templates, which are used to describe and provision AWS resources in a declarative manner.

### Features
- Create AWS resource effortlessly

### Installation
Dependencies to create the AWS resource:
- Make sure python3, jinja2, AWS-cli, jinja-cli is installed.
- Ensure the render-templates.py should be in place.

### Usage
Once you have the Jinja2 file and the Variable files ready here are the steps to create a stack.
- To render/parse the cloudofrmation jinja template to yaml use the below command
``` python3 render-templates.py <input_template_name>.j2 <variables_file_name>.yaml <output_cft_file_name>.yaml```
- Using the ```aws cloudformation create-stack --stack-name <stack name> --template-body file://<file name>``` create the stack for the resource.
- To delete the cloudformation stack ```aws cloudformation delete-stack --stack-name <stack name> --region <Region code>```

### Contributing
We welcome contributions from the community to enhance the AWS CloudFormation template. If you would like to contribute, please follow our guidelines outlined in the CONTRIBUTING.md file. You can submit feature requests, or pull requests to help us improve the template.

### License
