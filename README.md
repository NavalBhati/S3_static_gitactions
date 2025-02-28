🚀 Deploy a Static Website to AWS S3 Using GitHub Actions

IAM User policy

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
S3 Bucket Policy 
``` bash
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::Your-bucket-name/*"
        }
    ]
}
```

Ensure Your GitHub Secrets Are Set Correctly

Go to GitHub Repo → Settings → Secrets and Variables → Actions, and make sure you have the following secrets:

✅ AWS_ACCESS_KEY_ID → Your IAM user’s Access Key
✅ AWS_SECRET_ACCESS_KEY → Your IAM user’s Secret Key
✅ AWS_REGION → ap-south-1
✅ S3_BUCKET_NAME → my-static-site-gitaction-deployer280225

 .github/workflows/deploy-s3.yml file code
 
 ```bash
name: Deploy Static Website to S3

on:
  push:
    branches:
      - main  # Runs this workflow when changes are pushed to the 'main' branch

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Configure AWS Credentials
        uses: aws-actions/configure-aws-credentials@v2
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: ${{ secrets.AWS_REGION }}

      - name: Deploy to S3
        run: aws s3 sync . s3://${{ secrets.S3_BUCKET_NAME }} --delete
```

Check the Deployment Status

1️⃣ Go to your GitHub Repository.
2️⃣ Click on the “Actions” tab.
3️⃣ Look for the latest workflow run.
4️⃣ If successful, your static website should be live on S3! 🎉
