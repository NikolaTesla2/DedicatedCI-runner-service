## DedicatedCI Runner Service – Quickstart Guide
## 1️⃣ GitHub/GitLab Repository preparation

 - Push your project code to GitHub or GitLab.
 - Make sure your repository is private or trusted, because the runner will execute your code.

## 2️⃣ Add Runner

- Contact us to get your runner registration token.
- Go to your repo settings → Actions → Runners → Add self-hosted runner.
- Follow the instructions to register the runner on your VM.
- Use the label we provide, e.g.: customer-123456

## 3️⃣ Create Workflow File

- Create a workflow file in your repo: .github/workflows/build.yml
- Example for Node.js:

```yaml
name: CI Build
on:
  push:
    branches: [main]
  workflow_dispatch:

jobs:
  build:
    runs-on: [self-hosted, linux, customer-A]
    steps:
      - uses: actions/checkout@v3
      - name: Install dependencies
        run: npm install
      - name: Run build
        run: npm run build
      - name: Upload artifacts
        uses: actions/upload-artifact@v3
        with:
          name: build-output
          path: dist/
```
- Replace steps with your language stack if needed (Java, Rust, Android…).

## 4️⃣ start Build

- Automatic: push code → workflow triggers automatically
- Manual: in GitHub, click Actions → Your Workflow → Run workflow
- Logs and artifacts will appear in the GitHub interface.

## 5️⃣ Best Practices

- Keep secrets secure: don’t commit .env files, use GitHub secrets.
- Workspace cleanup: Runner deletes workspaces after each job automatically.
- solation: Each customer runs in their own VM → safe from other builds.

## ✅ That’s it!

- Repo ready ✅
- Runner registered ✅
- Workflow configured ✅
- Push or click → build starts ✅

Now you have your dedicated CI runner running your builds securely and efficiently.
