# 🖥️ Static Website Hosting on AWS  
**Personal Project by Ntsako M. Mabunda**

This project is part of my AWS learning journey. It demonstrates how I manually hosted a static website using **Amazon S3**, with optional enhancements using **CloudFront** for CDN and **Route 53** for a custom domain. Every step was performed manually to strengthen my understanding of AWS services and the website deployment process.

---

## 📌 Project Goals

- ✅ Host a static website using Amazon S3
- ✅ Understand S3 permissions and bucket policies
- ✅ (Optional) Use CloudFront for better performance and HTTPS
- ✅ (Optional) Connect a custom domain using Route 53

---

## 🧾 Overview

- **Tech stack**: HTML, CSS, JavaScript  
- **AWS services used**: S3, CloudFront (optional), Route 53 (optional)  
- **Project purpose**: Learn and showcase static web hosting on AWS  
- **Live URL**:  
  `http://ntsakomilen-static-site.s3-website-us-east-1.amazonaws.com/`

---

## 🔧 Tools & Services

- **Amazon S3** – For static website hosting  
- **AWS CLI** – To deploy from terminal  
- **(Optional) CloudFront** – For CDN and HTTPS support  
- **(Optional) Route 53** – For custom domain and DNS management  

---

## 🪜 Step-by-Step Deployment

### 1️⃣ Create the S3 Bucket

1. Logged into the [AWS S3 Console](https://s3.console.aws.amazon.com/s3/).
2. Created a bucket named `ntsakomilen-static-site`.
3. Unchecked **Block all public access**.
4. Enabled static website hosting in the **Properties** tab.

---

### 2️⃣ Upload Website Files

I uploaded the static site files into the `ntsakomilen-static-site` S3 bucket.

#### `index.html` – Main Homepage

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Welcome | My Site</title>
</head>
<body>
  <h1>Welcome to My Website</h1>
  <p>This is a basic HTML homepage.</p>
</body>
</html>
```

#### `error.html` – Custom 404 Page

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Error 404</title>
</head>
<body>
  <h1>404 - Page Not Found</h1>
  <p>Oops! The page you're looking for doesn't exist.</p>
  <a href="index.html">Return Home</a>
</body>
</html>
```

---

### 3️⃣ Deploy via AWS CLI

Using the AWS CLI, I uploaded all files to the S3 bucket:

```bash
aws s3 sync ./static-site s3://ntsakomilen-static-site
```

This command synced my local folder to the S3 bucket, making the site live.

---

### 4️⃣ (Alternative) Manual Upload via Console

1. Navigate to your S3 bucket.
2. Click **Upload**, then add your `index.html`, `error.html`, and assets.
3. Click **Upload** to finish.

This method is ideal for those unfamiliar with the CLI.

---

### 5️⃣ Enable Static Website Hosting

1. Open your bucket in the AWS S3 console.
2. Go to the **Properties** tab → Static Website Hosting → **Edit**.
3. Enable hosting and specify:
   - Index document: `index.html`
   - Error document: `error.html`
4. Save changes.

A public endpoint is generated (e.g., `http://bucket-name.s3-website-region.amazonaws.com/`).

---

### 6️⃣ Update Bucket Policy for Public Access

To make the site accessible to everyone:

1. Go to the **Permissions** tab of your bucket.
2. Under **Bucket Policy**, paste the following JSON:

```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Sid": "PublicReadGetObject",
    "Effect": "Allow",
    "Principal": "*",
    "Action": "s3:GetObject",
    "Resource": "arn:aws:s3:::ntsako-static-site/*"
  }]
}
```

✅ Now, your site is fully accessible via the public S3 URL.

---

## 🌐 Live Site

Access the project here:

```
http://ntsakomilen-static-site.s3-website-us-east-1.amazonaws.com/
```

---

## 🏁 Final Notes

This project was an excellent hands-on exercise to practice:

- Manual deployment of static sites
- Permission and policy management
- Command-line interactions with AWS

I plan to further enhance this setup with CloudFront and Route 53 integration in future projects.

---
