# 创建安全组 — 对应职位要求"security access controls"
resource "aws_security_group" "eda_server_sg" {
  name        = "eda-server-sg"
  description = "Security group for EDA design server"

  # 只允许内网 SSH（模拟公司 VPN 访问）
  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["10.0.0.0/8"]
    description = "SSH from corporate VPN only"
  }

  # 允许所有出站流量（下载EDA工具更新）
  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }

  tags = { Name = "EDA Server SG" }
}

# 创建 EC2 实例（模拟 EDA Linux 工作站）
resource "aws_instance" "eda_workstation" {
  ami           = "ami-098e39bafa7e7303d"  # Amazon Linux 2023 (us-east-1)
  instance_type = "t3.micro"

  vpc_security_group_ids = [aws_security_group.eda_server_sg.id]

  # 用户数据脚本：自动安装基础工具
  user_data = <<-EOF
    #!/bin/bash
    yum update -y
    yum install -y python3 git
    echo "EDA workstation ready" > /tmp/setup.log
  EOF

  tags = {
    Name    = "EDA-Workstation"
    Owner   = "Jeff"
    Purpose = "Terraform Learning"
  }
}

# 输出公网IP
output "instance_public_ip" {
  value = aws_instance.eda_workstation.public_ip
}
