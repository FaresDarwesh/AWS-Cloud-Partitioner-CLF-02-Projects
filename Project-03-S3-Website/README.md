# Project 3: Static Website Hosting on S3

## Objective
Host a static website using Amazon S3 without needing a server.

## AWS Services Used
- S3 (Simple Storage Service)
- Route 53 (optional - for custom domain)

## Steps
1. Create S3 Bucket
2. Upload `index.html` and `error.html`
3. Enable "Static website hosting" in Properties
4. Set Bucket Policy to allow public read
5. Uncheck "Block all public access"
6. Access website via S3 Endpoint URL

## Files Used
- `index.html` - Main page
- `error.html` - Error page (404)

## What I Learned
- S3 can host websites without EC2
- Bucket Policy (JSON) for public access
- Static vs Dynamic websites
- S3 Website Endpoint URL

## Screenshot
![S3 Website](screenshots/s3-website.png)

## Next
Project 4: Mounting an EBS Volume 💾
