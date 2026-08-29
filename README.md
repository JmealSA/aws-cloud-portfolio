# AWS Cloud Portfolio

A small portfolio site I built and deployed while learning AWS.

I wanted to keep this project simple and understand the services I was using instead of adding a bunch of AWS services just for the sake of it. The website is stored in a private S3 bucket and served through CloudFront.

## Live Site

https://d112dkejk8zr2b.cloudfront.net

## AWS Services

- Amazon S3
- Amazon CloudFront
- S3 bucket policies
- CloudFront Origin Access Control (OAC)

## How It Works

```text
User
  |
  v
CloudFront
  |
  v
Private S3 Bucket
  |
  +-- index.html
  +-- styles.css
  +-- app.js
```

The website files are stored in S3, but the bucket itself is not public.

CloudFront is allowed to retrieve the files from S3 and serve them to visitors. Direct requests to the S3 objects return `AccessDenied`.

This lets the site stay publicly accessible without making the S3 bucket public.

## Project Structure

```text
aws-cloud-portfolio/
├── frontend/
│   ├── index.html
│   ├── styles.css
│   └── app.js
├── aws/
│   └── cloudfront-bucket-policy.json
├── docs/
│   ├── setup-notes.md
│   └── interview-notes.md
├── .gitignore
└── README.md
```

## Deployment

I created an S3 bucket and uploaded the frontend files to the root of the bucket.

Public access to the bucket is blocked.

I then created a CloudFront distribution with the S3 bucket as its origin and allowed CloudFront to access the private bucket.

The default root object is:

```text
index.html
```

Once the distribution finished deploying, the site became available through the CloudFront domain.

## Testing the Setup

I tested both ways of accessing the site.

```text
CloudFront URL  -> Website loads
S3 Object URL   -> AccessDenied
```

This confirmed that visitors are getting the site through CloudFront and cannot access the S3 files directly.

## Updating the Site

When I make changes to the frontend, I upload the updated files to S3.

If CloudFront is still serving an older cached version, I can create an invalidation for:

```text
/*
```

That forces CloudFront to retrieve the updated files.

## What I Learned

This project helped me understand how S3 and CloudFront work together.

S3 is responsible for storing the files, while CloudFront is responsible for delivering them to users.

The biggest thing I learned was that hosting a public website does not mean the S3 bucket itself needs to be public. CloudFront can be given permission to access the bucket while direct public access stays blocked.

I also got hands-on experience configuring a CloudFront distribution, working with bucket permissions, testing access restrictions, and deploying changes through the AWS console.

## Next Steps

Some things I may add later:

- Custom domain
- Route 53
- AWS Certificate Manager
- CloudWatch monitoring
- Automatic deployment from GitHub