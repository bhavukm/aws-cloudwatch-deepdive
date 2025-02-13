# aws-cloudwatch-deepdive
All about CloudWatch Concepts

![image](https://github.com/user-attachments/assets/b2e417bf-ccfe-46d8-ba47-635ceea3b2bf)


![image](https://github.com/user-attachments/assets/cd18f2fa-dde7-454a-a56c-0339ef499fb7)

![image](https://github.com/user-attachments/assets/4285da38-53fd-4ad6-bad4-ca99e994b327)

Steps to Install and Configure CloudWatch and amazon-ssm agents:

1. Launch an AWS EC2 Instance with Amazon Linux AMI.
2. Create an IAM Role with 2 policies (aws-iam-ssm-policy and aws-iam-cloudwatch-policy present in this repo). Attach the IAM Role to the EC2 Instance.
3. SSH to the EC2 Instance.
4. Download, Install, and Configure the agents:
   
wget https://s3.us-east-1.amazonaws.com/amazoncloudwatch-agent-us-east-1/amazon_linux/amd64/latest/amazon-cloudwatch-agent.rpm

sudo yum install -y https://s3.amazonaws.com/ec2-downloads-windows/SSMAgent/latest/linux_amd64/amazon-ssm-agent.rpm

sudo systemctl start amazon-ssm-agent

sudo systemctl status amazon-ssm-agent

sudo rpm -U ./amazon-cloudwatch-agent.rpm

sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard

sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -m ec2 -a status

sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -m ec2 -a start

ps -ef |grep -i cloudwatch

Additionally, if you want to setup a CloudWatch Alarm for EC2 Memory Usage Threshold breach (Example: >=20%), use the following commands to increase memory usage on your EC2 Instance:

sudo yum install stress-ng -y

stress-ng --vm-bytes $(awk '/MemFree/{printf "%d\n", $2 * 0.9;}' < /proc/meminfo)k --vm-keep -m 1

To increase CPU usage on your EC2 Instance, use the following commands:

sudo yum install stress -y

stress --cpu 1 --timeout 800 &
