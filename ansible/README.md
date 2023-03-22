# Ansible image
## Use on Windows
docker run -v ${PWD}:/work kenwdelong/ansible:2.7.1 test.yml

### Use on Amazon Linux 2023
aws ecr-public get-login-password --region us-east-1 | sudo docker login --username AWS --password-stdin public.ecr.aws
https://gallery.ecr.aws/amazonlinux/amazonlinux
sudo docker pull public.ecr.aws/amazonlinux/amazonlinux:2023.0.20230315.0

