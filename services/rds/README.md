# AWS RDS using CloudFormation template

## Overview
This CloudFormation template is designed to deploy an Amazon RDS instance with various configurable parameters. It provides a flexible and automated way to create and manage your relational database on AWS.

## parameters
1.**Environment**
  - Type: String
  - Description: Environment name
  - Default: "{{ environment }}"

2.**Region**
  - Type: String
  - Description: AWS Region
  - Default: "{{ region }}"

3.**RdsName**
  - Type: String
  - Description: The name of the RDS instance
  - Default: "{{ rds_name }}"

4.**RdsStorage**
  - Type: Number
  - Description: The size of the database (in GB)
  - MinValue: 20
  - MaxValue: 16384
  - Default: "{{ rds_storage }}" ConstraintDescription: Must be between 20 and 16384 GB.

5.**EngineType**
  - Type: String
  - Description: The database engine to use
  - Default: "{{ engine_type }}"

6.**EngineVersion**
  - Type: String
  - Description: The engine version to use
  - Default: "{{ engine_version }}"

7.**DbInstanceClass**
  - Type: String
  - Description: The instance type of the RDS instance
  - Default: "{{ db_instance_class }}"

8.**DbMasterUsername**
  - Type: String
  - Description: Username for the master DB user
  - Default: "{{ db_master_username }}"

9.**DbMasterPassword**
  - Type: String
  - Description: Password for the master DB user
  - Default: "{{ db_master_password }}"
  - NoEcho: true

10.**VpcId**
  - Type: AWS::EC2::VPC::Id
  - Description: The ID of the VPC to deploy the RDS instance in
  - Default: "{{ vpc_id }}"

11.**SecurityGroupId**
  - Type: String
  - Description: The ID of the VPC security group to associate with the RDS instance
  - Default: "{{ security_group_id }}"

12.**MultiAzDeployment**
  - Type: String
  - Description: Specifies if the RDS instance is multi-AZ
  - Default: "{{ multi_az_deployment }}"

13.**PublicAccess**
  - Type: String
  - Description: Specifies if the RDS instance is publicly accessible
  - Default: "{{ public_access }}"

14.**SubnetName**
  - Type: String
  - Description: Subnet name
  - Default: "{{ subnet_name }}"

15.**SubnetGroup**
  - Type: String
  - Description: Name of the DB subnet group. The DB instance will be created in the VPC associated with the DB subnet group. If unspecified, it will be created in the default VPC
  - Default: "{{ subnet_group }}"

16.**ParameterGroup**
  - Type: String
  - Description: Name of the DB parameter group to associate or create
  - Default: "{{ parameter_group }}"

17.**ParameterGroupNew**
  - Type: String
  - Description: New parameter group
  - Default: "{{ parameter_group_new }}"

18.**OptionGroup**
  - Type: String
  - Description: Name of the option group
  - Default: "{{ option_group }}"

19.**OptionGroupNew**
  - Type: String
  - Description: A list of options to apply
  - Default: "{{ option_group_new }}"

20.**Encryption**
  - Type: String
  - Description: RDS storage encryption. Master key IDs and aliases appear in the list after they have been created using the AWS Key Management Service console
  - Default: "{{ encryption }}"

21.**LogExports**
  - Type: String
  - Description: Select 'yes' if you need to export logs to CloudWatch
  - Default: "{{ log_exports }}"



## Conditions
- **IsMultiAzDeployment:** Checks if the multi-AZ deployment is enabled.
- **IsPublicAccess:** Checks if public access is enabled.
- **IsEncryptionRequired:** Checks if encryption is required.
- **IsLogExportEnabled:** Checks if log export to CloudWatch is enabled.
- **IsOracleEngine**, **IsMariaDBEngine**, **IsMySQLEngine**, **IsPostgresEngine**, **IsSqlServerEngine:** Checks the database engine type.
- **IsMultiOptionGroup:** Checks if multiple option groups are specified.
- **IsParameterGroupNull**, **IsOptionGroupNull:** Checks if parameter and option groups are specified or null.
- **IsSubnetGroupPresent**, **IsSubnetGroupNull:** Checks if subnet group is specified or null.
- **ShouldEnablePublicAccess:** Checks if public access should be enabled based on the database engine type.

## Resources

### RdsInstance
- Type: AWS::RDS::DBInstance
- Properties: Defines the configuration of the RDS instance, including engine, storage, security groups, multi-AZ deployment, and other settings.

### RdsSecurityGroupIngress
- Type: AWS::EC2::SecurityGroupIngress
- Condition: ShouldEnablePublicAccess
- Properties: Configures security group ingress rules to allow public access to the RDS instance based on the selected database engine.

## Rendering CFT Template
- It's important to note that the actual values for the parameters and Jinja2 variables must be provided when creating a CloudFormation stack using this template. These values will determine the specific configuration of the stack.
- To render/parse the CloudFormation jinja template to yaml use the below command
```
python3 render-templates.py <input_template_name>.j2 <variables_file_name>.yaml <output_cft_file_name>.yaml
```

## Usage
- From the above command the CFT template file(<output_cft_file_name>.yaml) will be generated, which can be used to create the stack for Target Group.
