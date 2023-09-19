# Prequiste
You must have base64 encode/decode installed on your machine.
You must have your AWS credentials profile setup. (Role to assume can be defined in playbook)
You must have AWS Cli tool installed locally.
You must have Python3 and boto3 installed.

## For Target Hosts (No Access)

This playbook is used to set user-data on aws linux instances in order to provide Platform Operation teams common access to AWS EC2 instances.  In order for the changes to be applied by user-data a restart of the instance is required.  

### This playbook does the following
- Stop ec2 instance
- Add user-data specified in UserData.base64.txt. UserData.txt is the same, but a human readable file
- Start the instance

## Variables

cli_iid = instance id of the instance that will be re-keyed
cli_profile = profile name that uses the role locally in your config file.
region = the AWS region where the instance exists. (e.g. us-east-1)
account = Account number of the account that you are assuming role into
iam_role = name of the role being used not the full ARN of the resource.
ssh_user = default user or known user on the AMI or instance. #VERY IMPORTANT (user must exist already on instance or be default user for OS AMI)#
ssh_pub_key = full pubkey minus the ssh-rsa and space value associated with your private key. You also do not need the hostname in the pubkey file.

### run the playbook and specify instance and profile
`ansible-playbook -i hosts aws_ec2_rekey.yml -e"cli_iid=i-09f3366e33179e89c" -e"cli_profile=924339635232" -e"account=924339635232" -e"iam_role=plops-admin-sysops" -e"region=us-east-1"  -e"ssh_pub_key=XXXXXX2EAAAADAQABAAABAQDU3PEy/5PKO/bApFAPeTz64uu5RGbUVRdsDfbN+8BSEzirfFgFPSodnmRJtF50DLtSFuDyZ3lEC9wY0Jddhn9MY0XXXXXXXXXXrAay1Awu2wjjVkrJaIpBWHBCLtoJSrbnlImyIg3VqdIMB9rdxVPYj1zsM3IJxoohDL06xGUmPcWNMOmgbKiP3k73WJenPzTPniU/J8Akhdc2jMQDqqC7ZRP8aomr8fKfSHA8l1eiz3Vsd9mVqlNsmR/V/UComFtgiYe7JRi0MXXXXX" -e"ssh_user=centos"`

**Confirm Security groups for proper ssh access**
Port range | 	Protocol |   Source   | 	Security groups
  722 	      TCP	     212.42.176.235/32	  SSH Access
  722	        TCP	     12.116.165.150/32	  SSH Access
  722	        TCP	     185.19.208.91/32	    SSH Access
  722	        TCP	     38.140.8.98/32	      SSH Access
  722	        TCP	     65.158.245.42/32	    SSH Access
