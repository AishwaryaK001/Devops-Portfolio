Deploy to AWS S3 (Static Website Hosting)

Follow these steps to host the static site on S3 and make it publicly accessible.

🧭 Step 1: Create a Simple Portfolio Page (index.html)
    Copy the HTML + CSS code directly into a file named index.html.

🪣 Step 2: Host It on AWS S3 (Static Website)
    Here’s how to host it publicly:
    1. Log in to AWS Console → S3
    2. Click Create Bucket
    3. Name it (e.g., aishwarya-portfolio)
			 Region: Choose nearest to you
			 Uncheck “Block all public access”
			 Acknowledge the warning → Create bucket
		4. Click your bucket → Upload → Add index.html
		5. Go to Properties → Static website hosting
			 Enable it
			 Choose “Host a static website”
			 Set Index document: index.html
			 Save changes
6. Copy the Bucket website endpoint (your public URL)

🔓 Step 3: Public Access Policy (Bucket Policy)
		Attach this policy to allow public read access:

		✅ S3 Bucket Policy
		Replace YOUR_BUCKET_NAME with your actual bucket name.

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

		To apply:
		1. Go to your bucket → Permissions → Bucket Policy
		2. Paste the above JSON
		3. Replace YOUR_BUCKET_NAME
		4. Save
		
✅ Step 4: Test It
		Visit your S3 Static Website URL
		You should see your portfolio live! 🎉
