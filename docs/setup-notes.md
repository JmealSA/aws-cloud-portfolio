# Setup notes

These are the notes I would keep open while building the project.

## Build order

1. Create S3 bucket
2. Keep Block Public Access enabled
3. Upload frontend files
4. Create CloudFront distribution
5. Connect CloudFront to S3 using OAC
6. Add or confirm S3 bucket policy
7. Set `index.html` as the default root object
8. Test CloudFront URL
9. Test that direct S3 access is blocked
10. Push project to GitHub

---

## Names I would use

```text
S3 bucket: jamil-cloud-portfolio
CloudFront distribution: portfolio-distribution
```

The S3 bucket name may need a unique suffix.

---

## What to check if the site does not load

### AccessDenied

Check:

- CloudFront origin is the normal S3 bucket
- OAC is connected
- bucket policy has the correct CloudFront distribution ARN
- `index.html` is uploaded to the root
- default root object is `index.html`

### Old version keeps showing

CloudFront may still have a cached copy.

Create an invalidation:

```text
/*
```

Then refresh.

### CSS or JavaScript does not load

Make sure these are all at the bucket root:

```text
index.html
styles.css
app.js
```

The HTML currently expects those exact relative paths.

---

## Security points I should understand

- The S3 bucket is not public.
- CloudFront is allowed to read S3 through Origin Access Control.
- Visitors use CloudFront instead of direct S3 object URLs.
- No AWS keys are inside the frontend.
- The bucket policy only allows the CloudFront distribution to read objects.

---

## Git commands

```bash
git init
git add .
git commit -m "build AWS cloud portfolio"
git branch -M main
git remote add origin YOUR_GITHUB_REPO_URL
git push -u origin main
```

Normal later commits could be:

```bash
git commit -m "finish CloudFront setup"
git commit -m "update project section"
git commit -m "clean up mobile layout"
git commit -m "add AWS setup notes"
```
