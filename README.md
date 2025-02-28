🚀 Deploy a Static Website to AWS S3 Using GitHub Actions

```bash
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:GetObject",
                "s3:DeleteObject",
                "s3:ListBucket"
            ],
            "Resource": [
                "arn:aws:s3:::my-static-site-123",
                "arn:aws:s3:::my-static-site-123/*"
            ]
        }
    ]
}
```
