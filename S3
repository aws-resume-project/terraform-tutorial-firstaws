# main.tf — 你的第一个 Terraform 文件
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}

provider "aws" {
  region = "us-east-1"   # N.Virginia
}

# 创建 S3 Bucket
resource "aws_s3_bucket" "my_first_bucket" {
  bucket = "jeff-terraform-practice-2026"

  tags = {
    Name        = "Jeff Practice Bucket"
    Environment = "Learning"
    ManagedBy   = "Terraform"
  }
}

# 开启版本控制
resource "aws_s3_bucket_versioning" "versioning" {
  bucket = aws_s3_bucket.my_first_bucket.id
  versioning_configuration {
    status = "Enabled"
  }
}

# 阻止公开访问（安全最佳实践）
resource "aws_s3_bucket_public_access_block" "block" {
  bucket                  = aws_s3_bucket.my_first_bucket.id
  block_public_acls       = true
  block_public_policy     = true
  ignore_public_acls      = true
  restrict_public_buckets = true
}
