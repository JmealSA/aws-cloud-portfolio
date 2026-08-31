# AWS Cloud Portfolio

My personal portfolio website hosted on AWS.

I built this project to get hands-on experience deploying a real website with AWS. The frontend is written in HTML, CSS, and JavaScript, stored in a private S3 bucket, and served through CloudFront.

**Live site:** https://jamilsaad.com

## Architecture

```text
jamilsaad.com
      |
      v
   Route 53
      |
      v
CloudFront (HTTPS)
      |
      v
 Private S3 Bucket
      |
      +-- index.html
      +-- styles.css
      +-- app.js
```

## AWS Setup

### S3

The website files are stored in an Amazon S3 bucket with Block Public Access enabled.

The bucket is not directly accessible from the internet. I tested the S3 object URL separately and confirmed that direct requests return `AccessDenied`.

### CloudFront

CloudFront serves the website and acts as the public entry point.

I configured Origin Access Control (OAC) so CloudFront can retrieve files from the private S3 bucket without making the bucket public.

The distribution also handles caching and HTTPS traffic for the site.

### Route 53

I registered `jamilsaad.com` through Route 53 and configured the DNS records to point the domain to my CloudFront distribution.

### HTTPS

I created an SSL/TLS certificate with AWS Certificate Manager (ACM) and attached it to the CloudFront distribution.

The site is available over HTTPS at:

https://jamilsaad.com

## Tech Used

- HTML
- CSS
- JavaScript
- Amazon S3
- Amazon CloudFront
- Amazon Route 53
- AWS Certificate Manager
- CloudFront Origin Access Control

## Updating the Site

I make changes to the frontend locally and keep the project in GitHub.

For the current deployment process, updated frontend files are uploaded to S3. When needed, I create a CloudFront invalidation so the latest version is served instead of a cached copy.

## What I Learned

This project gave me experience working with AWS outside of just tutorials and documentation.

The main thing I wanted to understand was how different AWS services fit together. S3 handles the storage, CloudFront delivers the site, Route 53 handles the domain and DNS, and ACM provides the certificate for HTTPS.

It also helped me understand why a public website doesn't require a public S3 bucket. CloudFront can be given access to the bucket while direct access to the files stays blocked.
