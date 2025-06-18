## 📌 Project Overview

This project is a personal portfolio website hosted on AWS S3 using static website hosting. It demonstrates my understanding of AWS core services like S3, IAM, GitHub Actions, and infrastructure security principles.

The site is deployed automatically via CI/CD from a GitHub repo to an S3 bucket

# ⚙️ Technologies Used

- **Amazon S3** – Static website hosting
- **IAM** – Permissions and policies for access control
- **GitHub Actions** – CI/CD deployment pipeline
- **GitHub Secrets** – Secure handling of AWS credentials
- **WSL (Ubuntu on Windows)** – Dev environment for Git and Linux CLI

## 🛠️ Setup Instructions

1. Create an S3 bucket 
2. Block all public access to the bucket.
3. Create Cloudfront distribution
4. on origin create a new Origin Access identity to access the bucket
5. Set defualt root object on cloudfront configurations
6. Set only cloudfront distribution to access the website and update bucket policy
7. Set up version control using git locally on a WSL and push any changes to a github repo.
8. For CI/CD use a .yaml script to set up a trigger on github actions to update the
   code files in the s3 bucket. This ensures seamless updates to the webpage avioding
   manually uploading new files on the s3 bucket  everytime we are adding a new feature.
9. Set up GitHub Secrets(ensures that credentials are not included in the .yml script for security purposses):
    - `AWS_ACCESS_KEY_ID`
    - `AWS_SECRET_ACCESS_KEY`
    - `AWS_REGION`
    - `S3_BUCKET_NAME`
10. Push to the `master` branch to trigger deployment
  
## 📁 Repo Structure

.
├── website/
│ ├── index.html
│ └── style.css
├── .github/
│ └── workflows/
│ └── deploy.yml
└── README.md

💥 Challenges Faced & Lessons Learned
🔐 GitHub Actions + IAM
 -Initial workflow errors due to missing secret values.
 -Learned how to generate and scope IAM user access keys for GitHub CI/CD.
 
📦 **CloudFront Struggles**
-Spent days trying to configure CloudFront and Origin Access Control (OAC)
-Faced AccessDenied errors, invalidations not reflecting updates, and URL confusion.
-Changes not reflect intially before adding the deployment script were due to cache on cloudfront, 
 which needs invalidations ater changes for the changes to reflect on the webpage.
-After added invalidating cloudfront cache after s3 sync so the changes may reflect but
 got access denied. After troubleshooting using the isolation method of troubleshooting each resource 
 to identify the root of the problem. Cloudfront could not get the updated file because the github repo
 included the file path when sync the files to the s3 bucket and the defualt root was index.html 
 which lead to cloudfront not reachiing the bucket. the error is actually not fount but cloudfront uses
 error musking to hide the error from the s3 bucket behind it. That resolved the access denied issue and the website was served correctly
-Learned how to read S3 bucket policies and troubleshoot IAM conditions.

⚔️ **Git Issues on WSL**
Merge conflicts when syncing with GitHub.
Solved by practicing git add, git status, and conflict resolution using CLI.

🧠 **What I Learned**
-Real-world CI/CD setup with GitHub Actions
-IAM roles and least-privilege principles
-S3 static website hosting quirks and limitations
-How caching and object invalidation work
-Patience with cloud services 😅

🙋‍♂️ **Author**
**Samukelo Mnguni**
🧑‍💻 Junior BI / Cloud Developer
🌍 GitHub Profile
