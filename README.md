# AWS Cloud Portfolio

A personal portfolio website that I built and deployed using AWS.

I made this project to get hands-on experience with AWS instead of only reading about cloud services. The website is stored in a private S3 bucket and delivered through CloudFront. I also connected my own domain using Route 53 and added HTTPS using an AWS certificate.

## Live Website

https://jamilsaad.com

## Technologies Used

### Frontend
- HTML
- CSS
- JavaScript

### AWS
- Amazon S3
- Amazon CloudFront
- Amazon Route 53
- AWS Certificate Manager (ACM)
- CloudFront Origin Access Control (OAC)

## How It Works

```text
User
  |
  v
jamilsaad.com
  |
  v
Route 53
  |
  v
CloudFront + HTTPS
  |
  v
Private S3 Bucket
  |
  +-- index.html
  +-- styles.css
  +-- app.js
```

## What I Set Up

### Amazon S3

The website files are stored in an S3 bucket.

The bucket is private and Block Public Access is enabled. Opening the S3 object URL directly returns an Access Denied response.

### Amazon CloudFront

CloudFront is the public entry point for the website.

I configured CloudFront to access the private S3 bucket using Origin Access Control (OAC). This allows CloudFront to serve the files without making the S3 bucket public.

I also set `index.html` as the default root object.

### Route 53

I registered and configured `jamilsaad.com` using Route 53.

The domain has an alias record that routes traffic to my CloudFront distribution.

### HTTPS

I created an SSL/TLS certificate through AWS Certificate Manager and connected it to the CloudFront distribution.

The portfolio can be accessed securely through:

https://jamilsaad.com

## Updating the Website

When I make changes to the website:

1. Update the HTML, CSS, or JavaScript locally.
2. Upload the updated files to the S3 bucket.
3. Create a CloudFront cache invalidation if the old version is still being served.

## Project Structure

```text
aws-cloud-portfolio/
|
|-- frontend/
|   |-- index.html
|   |-- styles.css
|   `-- app.js
|
|-- aws/
|   `-- cloudfront-bucket-policy.json
|
|-- docs/
|   |-- setup-notes.md
|   `-- interview-notes.md
|
|-- .gitignore
`-- README.md
```

## What I Learned

This project gave me hands-on practice with:

- Hosting static files with S3
- Keeping an S3 bucket private
- Using CloudFront to deliver a website
- Configuring CloudFront Origin Access Control
- Connecting a custom domain with Route 53
- Setting up HTTPS with AWS Certificate Manager
- Working with DNS records
- Using CloudFront cache invalidations
- Setting up an AWS budget to keep track of costs

## Why I Built This

I wanted a small AWS project that I could build myself and understand from start to finish.

It helped me understand how AWS services can work together to host and securely deliver a real website instead of only learning the concepts individually.