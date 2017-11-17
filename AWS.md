Getting Started with AWS
========================
* Getting Started with the AWS Managment Console: http://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/getting-started.html
* Getting Started Resource Center: https://aws.amazon.com/getting-started/

## Login credentials
We will provide you with the following credentials via VAULT:
* `LoginUrl` - AWS Management Console login URL, e.g. _https://<account-id>.signin.aws.amazon.com/console_
* `Username` - AWS Management Console username, e.g. _team-X@hackovation.io_
* `Password` - AWS Management Console password, e.g. _ABC_

#### Creating access keys
To access the service programmatically, you will need to create access keys. You can find everything you need to know on how to do this here: http://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html#Using_CreateAccessKey

#### Configuring the AWS CLI tools
For the next example, we will need to have the AWS CLI installed and configured (https://aws.amazon.com/cli/).

After you have successfully installed the _awscli_, run
```
aws configure
```
and add your
* Access Key ID
* Secret Access Key
* Region (eu-west-1)
* Output Format (json)

.. to setup your environment.

## Example Instance

In this example, we will launch a single EC2 instance and then terminate it.

1. Create a new instance in _eu-west-1_ based on _Amazon Linux_
```
aws ec2 run-instances --image-id ami-760aaa0f --count 1 --instance-type t2.micro --region eu-west-1
```
Take note of the `InstanceId`.

Wait a few minutes until your instance is ready. You can see the status in the Management console or via the command line.

After the instance has been successfully launched, terminate it with the following command:

```
aws ec2 terminate-instances --instance-ids <InstanceId> --region eu-west-1
```

## Documentation
* Service Overview: https://aws.amazon.com/products/
* Service Documentation: https://aws.amazon.com/documentation/

## FAQ
