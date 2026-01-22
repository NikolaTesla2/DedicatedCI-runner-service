# DedicatedCI-runner-service

**Dedicated self-hosted GitHub/GitLab CI runner for fast, isolated builds. 
Ideal for freelancers and small dev teams. 
Best-effort service.**

---

## ⚡ Overview

This service allows you to run **GitHub/GitLab CI workflows** on a **dedicated VM** hosted by us.  
No shared queues, fully isolated, fast builds. Ideal for:

- Freelancers
- Small development teams
- Projects where local builds are slow

> **Note:** This is a Best-Effort service. Not for production-critical workloads.  
> The runner is isolated per customer; we do **not guarantee uptime or availability**.

---

## 🛠️ How It Works

1. You push your code to your GitHub/GitLab repository.
2. Your workflow references your **self-hosted runner label**:

```yaml
jobs:
  build:
    runs-on: [ self-hosted, linux, customer-A ]
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
