
# Assignment 1 – Amazon CloudFront CDN with Multiple S3 Origin

## 📘 Objective

Create a single CloudFront distribution to deliver content from two S3 website origins with path-based routing and a minimum 48-hour edge cache.

---

## 🪣 S3 Setup

**Bucket 1:** `my-bucket-1-for-devops-assignment`

* Enabled *Static Website Hosting*
* `index.html` content:

  ```
  Hello, CDN origin is working fine
  ```

**Bucket 2:** `my-bucket-2-for-devops-assignment`

* Enabled *Static Website Hosting*
* Folder `devops-folder/` with `index.html` content:

  ```
  Hello, CDN 2 origin is working fine
  ```

---

## 🌍 CloudFront Setup

* **Distribution type:** Single website
* **Origins:**

  * Origin A → S3 Bucket 1 (no path)
  * Origin B → S3 Bucket 2 (`/devops-folder`)
* **Behaviors:**

  * Default behavior → Origin A
  * Path pattern `devops-folder/*` → Origin B
* **Cache policy:** Custom (Min TTL = 172800 seconds = 48 hours)
* **Default root object:** `index.html`
* **No CNAMEs used** (default CloudFront domain)

---

## ✅ Verification

| URL                                           | Output                            |
| --------------------------------------------- | --------------------------------- |
| [https://d3bl7eemi7lzor.cloudfront.net/](https://d3bl7eemi7lzor.cloudfront.net/)        | Hello, CDN origin is working fine |
| [https://d3bl7eemi7lzor.cloudfront.net/devops-folder/](https://d3bl7eemi7lzor.cloudfront.net/devops-folder/) | Hello, CDN 2 origin is working fine |
