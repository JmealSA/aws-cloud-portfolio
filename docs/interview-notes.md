# Interview notes

These are talking points, not something I would memorize word for word.

## 30 second explanation

I built a small portfolio website and deployed it on AWS while I was learning the platform. The website files are stored in S3, but I kept the bucket private. CloudFront sits in front of it and serves the site over HTTPS. I used Origin Access Control so CloudFront could read the bucket without making the files directly public.

## Why did you use S3?

The site is static, so it only needs storage for files like HTML, CSS, and JavaScript.

There was no reason to run a server for the first version.

## Why CloudFront?

CloudFront gives the website an HTTPS endpoint and caches the files closer to users.

It also lets me keep the S3 bucket private instead of exposing the bucket directly.

## What is Origin Access Control?

It is the permission setup that lets CloudFront access the private S3 origin.

The bucket policy allows the CloudFront distribution to read the objects.

## Why not just make the S3 bucket public?

I wanted the public entry point to be CloudFront.

Keeping S3 private gave me practice with permissions and is a cleaner setup than making all of the files directly public.

## What does caching mean here?

CloudFront can keep copies of the website files at edge locations.

That means every request does not always have to go back to the S3 origin.

When I update the website, I can create an invalidation so CloudFront fetches the newer files.

## Did you use a backend?

No.

I intentionally kept the first version static because I wanted to understand S3 and CloudFront before adding more services.

That is a good answer. Do not pretend the project has Lambda or an API if it does not.

## What would you add next?

A few realistic options:

- custom domain
- Route 53
- ACM certificate
- CloudWatch monitoring
- GitHub Actions deployment

Pick one or two depending on the conversation.

## What was the main thing you learned?

A normal answer:

> The biggest thing I learned was how the permissions fit together. At first I thought a public website meant the S3 bucket had to be public. After setting up CloudFront and OAC, I understood that CloudFront can be the public layer while S3 stays private.

## Things I should not claim

Do not say:

- I am AWS certified before passing the exam.
- I built a production enterprise system.
- I used Lambda or API Gateway in this project.
- The project can never cost money.
- I set up CI/CD if I did not.

The goal is to be able to explain exactly what I built.
