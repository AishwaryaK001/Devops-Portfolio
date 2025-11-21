# Basic CI/CD pipeline using Bitbucket Pipelines with Node.js #
**Step 1 — Create a new Bitbucket repo & a tiny Node.js app (locally)**

Create a folder and two files (index.js, package.json) that satisfy your requirements.
```
# make a new project folder and enter it
mkdir cicd-demo && cd cicd-demo

# create index.js
console.log("Hello from CI/CD demo");

# create package.json with start and a test that always passes
{
  "name": "cicd-demo",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "start": "node index.js",
    "test": "echo \"Running tests\" && exit 0"
  }
}
```
**Step 2 — Initialize the git repo, commit locally**
```
git init
git add .
git commit -m "initial: simple Node.js demo for Bitbucket Pipelines"
```
**Step 3 — Create the remote repo on Bitbucket and connect it**

Log in to Bitbucket (bitbucket.org).

Click Create repository → give it a name like cicd-demo → choose Private/Public as you prefer → create.

After creation, Bitbucket will show clone URLs (SSH and HTTPS). 

Add the remote locally and push:

HTTPS
```
git branch -M main
git remote add origin https://<YOUR_BITBUCKET_USERNAME>@bitbucket.org/<YOUR_BITBUCKET_USERNAME>/cicd-demo.git
git push -u origin main
```
You must create the repo on Bitbucket (UI step). 

Then set origin and push the main branch which creates the remote branch and triggers Pipelines (once enabled).

**Step 4 — Add bitbucket-pipelines.yml with Build → Test → Deploy steps**

Create a file named bitbucket-pipelines.yml in the repo root and add the content given in yml file above.

- image: node:18 chooses Node 18 Docker image for all steps. Adjust if you need another Node version.

- The pipeline has three sequential steps: Build installs dependencies, Test runs npm test, Deploy just prints a placeholder message.

- npm ci || npm install uses npm ci when a lockfile exists but falls back to npm install.

Commit the file:
```
git add bitbucket-pipelines.yml
git commit -m "ci: add bitbucket-pipelines.yml with build/test/deploy steps"
git push
```
**Step 5 — Enable Pipelines in Bitbucket**

In the Bitbucket repo UI, go to Repository settings → Pipelines (or there's a left sidebar link Pipelines).

Click Enable Pipelines (toggle or button).

Optionally review and save.

- Pipelines are off by default. Enabling them lets Bitbucket read bitbucket-pipelines.yml and run builds on pushes.

**Step 6 — Trigger the pipeline (commit & push so it runs)**

Any push to the branch (e.g., main) will trigger the default pipeline. 
You already pushed earlier;
after enabling Pipelines, push again to be safe:
```
# after you made the pipeline file and committed
git push origin main
```
**Step 7 — Verify pipeline logs for Build → Test → Deploy**

In Bitbucket repo, click Pipelines in left sidebar.

You’ll see a list of pipeline runs. Click the run triggered by your push.

Inside a run, the steps are shown in order: Build, Test, Deploy. Click a step to view the real-time or finished logs.

<img width="600" height="600" alt="image" src="https://github.com/user-attachments/assets/630329ec-7115-4c3a-9b00-a55657957380" />

<img width="600" height="600" alt="image" src="https://github.com/user-attachments/assets/bb2339fd-8390-4258-95fb-121ad9690969" />

<img width="600" height="600" alt="image" src="https://github.com/user-attachments/assets/5edca55f-152d-42d2-9074-111322414e41" />


## Extend pipeline to build Docker image & push to Docker Hub

**1. Add Bitbucket Repository Variables**

In Bitbucket → Repo → Repository Settings → Pipelines → Repository variables
```
DOCKERHUB_USERNAME - your Docker Hub username
DOCKERHUB_PASSWORD - Docker Hub password or access token
DOCKERHUB_REPO - e.g. cicd-demo
```
**2. Add a Dockerfile to your project root**
```
FROM node:18
WORKDIR /app
COPY package*.json ./
RUN npm install --production
COPY . .
CMD ["node", "index.js"]
```
**3. Extended bitbucket-pipelines.yml Build → Test → Docker Build & Push**
```
image: node:18

pipelines:
  default:
    - step:
        name: Build
        caches:
          - node
        script:
          - echo "=== Installing dependencies ==="
          - npm ci || npm install

    - step:
        name: Test
        caches:
          - node
        script:
          - echo "=== Running tests ==="
          - npm test

    - step:
        name: Build & Push Docker Image
        services:
          - docker
        script:
          - echo "=== Docker Hub Login ==="
          - echo "$DOCKERHUB_PASSWORD" | docker login -u "$DOCKERHUB_USERNAME" --password-stdin

          - echo "=== Building Docker Image ==="
          - docker build -t $DOCKERHUB_USERNAME/$DOCKERHUB_REPO:latest .

          - echo "=== Pushing Docker Image ==="
          - docker push $DOCKERHUB_USERNAME/$DOCKERHUB_REPO:latest
```
**4. Verify in Docker Hub**

<img width="600" height="600" alt="image" src="https://github.com/user-attachments/assets/9d83b96d-cd42-4c3a-9d04-087b4d2ff28f" />

<img width="600" height="600" alt="image" src="https://github.com/user-attachments/assets/6cb16efa-f97c-4dde-8db5-ca910c6211ce" />


