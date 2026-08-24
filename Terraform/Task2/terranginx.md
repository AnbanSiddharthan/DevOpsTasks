## Create 2 EC2 instances on 2 different regions and install nginx using terraform script.


### Step 1 — Install AWS CLI

 ```bash
 sudo apt update
sudo apt install awscli -y
aws --version
```
### Step 2 — Check AWS authentication

```bash
 aws sts get-caller-identity
```
### Step 3 — Install Terraform

```bash
 sudo apt install -y gnupg software-properties-common
```

```bash
 wget -O- https://apt.releases.hashicorp.com/gpg | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg > /dev/null
```

```bash
 echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/hashicorp.list
```
### Step 4 — Create a new Terraform project

```bash
 mkdir terraform-nginx-two-regions
```

```bash
 nano main.tf
```
#### File content 
```bash
terraform {
  required_providers {
    aws = {
      source = "hashicorp/aws"
    }
  }
}

# ============================================================
# PROVIDERS
# ============================================================

provider "aws" {
  region = "eu-north-1"
}

provider "aws" {
  alias  = "us_east"
  region = "us-east-1"
}

# ============================================================
# UBUNTU AMI
# ============================================================

data "aws_ssm_parameter" "ubuntu_eu_north" {
  name = "/aws/service/canonical/ubuntu/server/24.04/stable/current/amd64/hvm/ebs-gp3/ami-id"
}

data "aws_ssm_parameter" "ubuntu_us_east" {
  provider = aws.us_east

  name = "/aws/service/canonical/ubuntu/server/24.04/stable/current/amd64/hvm/ebs-gp3/ami-id"
}

# ============================================================
# SECURITY GROUP - EU NORTH
# ============================================================

resource "aws_security_group" "nginx_eu_north" {
  name        = "nginx-eu-north-sg"
  description = "Allow HTTP traffic"

  ingress {
    description = "HTTP"
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }

  tags = {
    Name = "Nginx-EU-North-SG"
  }
}

# ============================================================
# SECURITY GROUP - US EAST
# ============================================================

resource "aws_security_group" "nginx_us_east" {
  provider    = aws.us_east
  name        = "nginx-us-east-sg"
  description = "Allow HTTP traffic"

  ingress {
    description = "HTTP"
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }

  tags = {
    Name = "Nginx-US-East-SG"
  }
}

# ============================================================
# EC2 - EU NORTH
# ============================================================

resource "aws_instance" "nginx_eu_north" {
  ami           = data.aws_ssm_parameter.ubuntu_eu_north.value
  instance_type = "t3.micro"

  vpc_security_group_ids = [
    aws_security_group.nginx_eu_north.id
  ]

  user_data = <<-EOF
    #!/bin/bash
    apt update
    apt install nginx -y
    systemctl enable nginx
    systemctl start nginx
  EOF

  tags = {
    Name = "Nginx-EU-North"
  }
}

# ============================================================
# EC2 - US EAST
# ============================================================

resource "aws_instance" "nginx_us_east" {
  provider      = aws.us_east
  ami           = data.aws_ssm_parameter.ubuntu_us_east.value
  instance_type = "t3.micro"

  vpc_security_group_ids = [
    aws_security_group.nginx_us_east.id
  ]

  user_data = <<-EOF
    #!/bin/bash
    apt update
    apt install nginx -y
    systemctl enable nginx
    systemctl start nginx
  EOF

  tags = {
    Name = "Nginx-US-East"
  }
}

```

### Step 5 — Initialize Terraform

```bash
terraform init
terraform validate
```
### Step 6 — Run Terraform plan

```bash
 terraform plan
```
### Step 7 — Create the instances

```bash
 terraform apply
```
### Step 8 — Verify the EC2 instances with AWS CLI

```bash
 aws ec2 describe-instances \
  --region eu-north-1 \
  --query 'Reservations[].Instances[].{ID:InstanceId,State:State.Name,Type:InstanceType,Name:Tags[?Key==`Name`].Value|[0],PublicIP:PublicIpAddress}' \
  --output table
```

```bash
 aws ec2 describe-instances \
  --region us-east-1 \
  --query 'Reservations[].Instances[].{ID:InstanceId,State:State.Name,Type:InstanceType,Name:Tags[?Key==`Name`].Value|[0],PublicIP:PublicIpAddress}' \
  --output table
```
### Step 9 — Verify Nginx

```bash
 curl http://13.62.228.46
```

```bash
curl http://3.235.109.184 
```

### Screenshots

<img width="1470" height="670" alt="image" src="https://github.com/user-attachments/assets/2e2ab5ff-afd0-40da-9bf2-a23157e0d7c4" />
<img width="1471" height="588" alt="image" src="https://github.com/user-attachments/assets/28ba05bb-621b-438b-9b0e-b00757eb3ed6" />
<img width="1477" height="583" alt="image" src="https://github.com/user-attachments/assets/4dbbeca0-681d-4dcb-91b3-e731f00e33d9" />




