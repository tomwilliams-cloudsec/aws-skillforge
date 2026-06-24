<<<<<<< HEAD
# ⬡ AWS SkillForge

> **My personal AWS learning hub** — certifications, hands-on projects, curated resources, and a cloud challenge generator. Hosted on S3 as a static site.

![AWS](https://img.shields.io/badge/Hosted_on-AWS_S3-FF9900?style=flat&logo=amazon-aws&logoColor=white)
![Static](https://img.shields.io/badge/Type-Static_Site-63B3ED?style=flat)
![No Backend](https://img.shields.io/badge/Backend-None-68D391?style=flat)
![localStorage](https://img.shields.io/badge/Storage-localStorage-B794F4?style=flat)

---

## 🚀 Live Features

| Feature | Description |
|---|---|
| **Certification Roadmap** | Visual timeline of my AWS cert journey with status indicators |
| **Service Tracker** | 28 AWS services — click to mark as practiced, progress saved locally |
| **Project Board** | Add projects, cycle statuses (Planning → In Progress → Complete → Paused) |
| **Resource Library** | Curated free + paid study materials with direct links |
| **Quick Tips** | Things I learned the hard way |
| **Cloud Challenge Generator** | Random beginner-to-intermediate AWS hands-on tasks |

---

## 🗂 Project Structure

```
aws-skillforge/
├── index.html          # Single-page app (all HTML, CSS, JS)
└── README.md           # This file
```

Everything is in one `index.html` file — no build step, no dependencies, no server needed.

---

## ☁️ Deploy to AWS S3

### 1. Create the S3 bucket

```bash
aws s3 mb s3://your-skillforge-bucket-name --region us-east-1
```

### 2. Enable static website hosting

```bash
aws s3 website s3://your-skillforge-bucket-name \
  --index-document index.html \
  --error-document index.html
```

### 3. Set bucket policy for public read

Create `bucket-policy.json`:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::your-skillforge-bucket-name/*"
    }
  ]
}
```

Apply it:

```bash
aws s3api put-bucket-policy \
  --bucket your-skillforge-bucket-name \
  --policy file://bucket-policy.json
```

### 4. Upload the site

```bash
aws s3 sync . s3://your-skillforge-bucket-name \
  --exclude ".git/*" \
  --exclude "README.md" \
  --exclude "bucket-policy.json"
```

### 5. Your site is live at:

```
http://your-skillforge-bucket-name.s3-website-us-east-1.amazonaws.com
```

---

## 🌐 Optional: Add CloudFront (HTTPS + CDN)

For HTTPS and faster global delivery:

```bash
aws cloudfront create-distribution \
  --origin-domain-name your-skillforge-bucket-name.s3-website-us-east-1.amazonaws.com \
  --default-root-object index.html
```

Or configure it in the AWS Console under CloudFront → Create Distribution.

---

## 🔄 Update the site

```bash
# After editing index.html:
aws s3 sync . s3://your-skillforge-bucket-name \
  --exclude ".git/*" \
  --exclude "README.md" \
  --exclude "bucket-policy.json"

# Optional: invalidate CloudFront cache
aws cloudfront create-invalidation \
  --distribution-id YOUR_CF_DISTRIBUTION_ID \
  --paths "/*"
```

---

## 🛠 Customizing

All site content lives in `index.html`. Key sections to update:

| Section | Where in code |
|---|---|
| Your name/tagline | `#hero` section |
| Gumroad/social links | `href` attributes in hero + footer |
| Services list | `const SERVICES = [...]` in `<script>` |
| Projects | `const DEFAULT_PROJECTS = [...]` — or add live via the UI |
| Resources | `#resources` section HTML |
| Challenge prompts | `const CHALLENGES = [...]` in `<script>` |
| Certification timeline | `.cert-track` HTML nodes |

### Adding a service

```js
{ id:'bedrock', name:'Bedrock', cat:'compute', icon:'🤖' },
```

### Adding a challenge

```js
{ text: 'Create a Step Functions workflow with 3 Lambda states and test execution.', diff:'intermediate', time:'~60 min', tags:['Step Functions', 'Lambda'] },
```

---

## 💾 Data & Privacy

All user data (practiced services, projects, challenge history) is stored in **browser localStorage only**. No analytics, no backend, no tracking. Each visitor's data is their own.

---

## 📌 Related

- 📘 [Cert to Salary Study Guides](https://certosalary.gumroad.com) — My AWS CLF-C02 study guide + free Well-Architected Framework breakdown
- 🏗️ [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/)
- 🎓 [AWS Skill Builder](https://skillbuilder.aws/)

---

*Built by Tom · Cert to Salary · Hosted on AWS S3*
=======
# aws-skillforge
>>>>>>> 4fbb8e56927de993ce1728ab1db549f6b88b562a
