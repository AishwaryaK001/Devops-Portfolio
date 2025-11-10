## 🚀 Deploy to AWS S3 (Static Website Hosting)

Follow these steps to **host your static portfolio website on Amazon S3** and make it publicly accessible.

---

### 🧭 Step 1: Create a Simple Portfolio Page (`index.html`)

Copy the HTML + CSS code directly into a file named **`index.html`**.

---

### 🪣 Step 2: Host It on AWS S3 (Static Website)

Here’s how to host it publicly:

1. **Log in** to the AWS Management Console → Go to **S3**
2. Click **Create Bucket**
3. **Configure your bucket:**
   - **Name:** e.g., `aishwarya-portfolio`
   - **Region:** Choose the nearest region
   - **Uncheck:** “Block all public access”
   - **Acknowledge** the warning → Click **Create bucket**
4. Open your bucket → **Upload** → Add your `index.html` file
5. Go to **Properties → Static website hosting**
   - Enable it
   - Choose **“Host a static website”**
   - Set **Index document:** `index.html`
   - Click **Save changes**
6. Copy the **Bucket website endpoint (your public URL)** — this will be your website link.

---

### 🔓 Step 3: Public Access Policy (Bucket Policy)

Attach this policy to your S3 bucket to allow **public read access**.

#### ✅ S3 Bucket Policy

> Replace `YOUR_BUCKET_NAME` with your actual S3 bucket name.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::YOUR_BUCKET_NAME/*"
    }
  ]
}
```

**To apply:**

  -	 Go to your bucket → Permissions → Bucket Policy
  -	 Paste the above JSON
  -  Replace YOUR_BUCKET_NAME
  -  Save
		
### ✅ Step 4: Test It**
		Visit your S3 Static Website URL
		You should see your portfolio live! 🎉

---

<p align="center">
  <img src="https://github.com/user-attachments/assets/a43ac513-77ce-41b6-8978-5bef32aa83c5" alt="AWS S3 Screenshot" width="600">
</p>

