# 创建 IAM 用户（模拟新入职工程师账号）
resource "aws_iam_user" "engineer" {
  name = "eda-engineer-01"
  tags = { Department = "ASIC Design" }
}

# 创建权限策略（只读 S3，不能删除）
resource "aws_iam_policy" "s3_read_only" {
  name        = "EDA-S3-ReadOnly"
  description = "Read-only access to EDA data bucket"

  policy = jsonencode({
    Version = "2012-10-17"
    Statement = [
      {
        Effect   = "Allow"
        Action   = ["s3:GetObject", "s3:ListBucket"]
        Resource = [
          aws_s3_bucket.my_first_bucket.arn,
          "${aws_s3_bucket.my_first_bucket.arn}/*"
        ]
      }
    ]
  })
}

# 将策略绑定到用户
resource "aws_iam_user_policy_attachment" "attach" {
  user       = aws_iam_user.engineer.name
  policy_arn = aws_iam_policy.s3_read_only.arn
}
