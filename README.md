# GitHub OSINT – Mini Cybersecurity Project Report

**Author:** Uday Kiran  
**Date:** 30-07-2025  

---

## 1. Introduction
In the modern software development world, publicly hosted repositories such as GitHub are often unintentionally used as a medium for exposing sensitive data.  
This project focuses on **Open Source Intelligence (OSINT)** gathering from public GitHub repositories, aiming to discover leaked credentials, API tokens, and secrets using a combination of **GitHub dorks** and **automated tools**.

---

## 2. Tools Used
- **Custom GitHub Dorks** – Manual search queries to find exposed secrets in code and files.
- **GitLeaks (v8.28.0)** – Automated tool for scanning Git repositories for secrets like API keys, tokens, and passwords.

---

## 3. Methodology

### Step 1: Target Selection
Selected various public GitHub repositories such as:
- `HariSekhon/Kubernetes-configs`
- `maxh33/showcase-twitter-clone`
- `fingerprintjs/fingerprintjs-pro-server-api-node-sdk`

### Step 2: Manual Dorking
Used GitHub search bar to run queries like:

filename:password.ini
kong_admin password
vercel token


### Step 3: GitLeaks Scan
Cloned the selected repository locally and ran:
```bash
gitleaks detect --source=. --report-path=gitleaks-report.json --report-format=json

4. Key Findings

Finding 1: Hardcoded Kong Credentials in Public Repository

Repo: HariSekhon/Kubernetes-configs

Credential: kong_admin / password

Risk: High – Default credentials could be used to access admin panels if unchanged.

Finding 2: Vercel and Deployment Secret Metadata Exposed

Repo: maxh33/showcase-twitter-clone

Secrets: VERCEL_TOKEN, JWT_SECRET_KEY, EMAIL_HOST_PASSWORD

Risk: High – If values are committed, attackers can exploit them.

Finding 3: Placeholder Secrets in Public Code

Repo: fingerprintjs/fingerprintjs-pro-server-api-node-sdk

Secret Example: <SECRET_API_KEY>

Risk: Medium – Even placeholders reveal potential attack surfaces.

Finding 4: GitLeaks Scan Result

Tool Used: GitLeaks v8.28.0

Repo Scanned: showcase-twitter-clone

Result: Secrets detected and logged in gitleaks-report.json

Risk: Medium/High depending on secrets found.

5. Screenshots

(Add screenshots here when uploading to GitHub, e.g. ![Kong credentials screenshot](screenshots/kong-creds.png))

6. Recommendations

Never commit secrets (passwords, tokens) to public repositories.

Add .env, .ini, or config files to .gitignore.

Use tools like GitLeaks and GitHub Secret Scanning to detect leaks early.

Rotate exposed secrets immediately.

Follow OWASP password storage best practices.

7. Conclusion

This mini project successfully identified multiple real-world examples of poor secret management in public GitHub repositories.
The use of GitHub dorking and GitLeaks proved effective in uncovering potentially exploitable issues, highlighting the need
for strong DevSecOps hygiene and automated secret scanning tools in the software development lifecycle.
