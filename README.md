# aws-cloudwatch-deepdive
All about CloudWatch Concepts

![image](https://github.com/user-attachments/assets/d09c8051-e1ed-4323-8193-328731847a21)

![image](https://github.com/user-attachments/assets/cd18f2fa-dde7-454a-a56c-0339ef499fb7)

![image](https://github.com/user-attachments/assets/4285da38-53fd-4ad6-bad4-ca99e994b327)

Steps to Install and Configure CloudWatch and amazon-ssm agents:
1. Launch an AWS EC2 Instance with Amazon Linux AMI and SSH to it.
2. Download, Install, and Configure the agents:
wget https://s3.us-east-1.amazonaws.com/amazoncloudwatch-agent-us-east-1/amazon_linux/amd64/latest/amazon-cloudwatch-agent.rpm
sudo rpm -U ./amazon-cloudwatch-agent.rpm
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard
systemctl status amazon-cloudwatch-agent.service
systemctl start amazon-cloudwatch-agent.service
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -m ec2 -a status
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -m ec2 -a start
ps -ef |grep -i cloudwatch
sudo yum install -y https://s3.amazonaws.com/ec2-downloads-windows/SSMAgent/latest/linux_amd64/amazon-ssm-agent.rpm
sudo systemctl start amazon-ssm-agent
sudo systemctl status amazon-ssm-agent

Additionally, if you want to setup a CloudWatch Alarm for EC2 Memory Usage Threshold breach (Example: >=20%), use the following commands to increase memory usage on your EC2 Instance:
sudo yum install stress-ng -y
stress-ng --vm-bytes $(awk '/MemFree/{printf "%d\n", $2 * 0.9;}' < /proc/meminfo)k --vm-keep -m 1
