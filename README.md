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

```
3. Our dedicated VM automatically picks up your job and runs it.
4. Build logs and artifacts are returned to your GitHub/GitLab interface.

## Example Workflows
**Node.js**
```yaml
jobs:
  build:
    runs-on: [ self-hosted, linux, customer-A ]
    steps:
      - uses: actions/checkout@v3
      - name: Install dependencies
        run: npm install
      - name: Build project
        run: npm run build
      - name: Upload artifacts
        uses: actions/upload-artifact@v3
        with:
          name: build-output
          path: dist/
```
**Java / Maven**
```yaml
jobs:
  build:
    runs-on: [ self-hosted, linux, customer-A ]
    steps:
      - uses: actions/checkout@v3
      - name: Set up JDK
        uses: actions/setup-java@v3
        with:
          java-version: '17'
      - name: Build
        run: mvn clean install
      - name: Upload artifacts
        uses: actions/upload-artifact@v3
        with:
          name: target
          path: target/
```
**Rust / Cargo**
```yaml
jobs:
  build:
    runs-on: [ self-hosted, linux, customer-A ]
    steps:
      - uses: actions/checkout@v3
      - name: Install Rust
        uses: actions-rs/toolchain@v1
        with:
          toolchain: stable
          override: true
      - name: Build
        run: cargo build --release
      - name: Upload artifacts
        uses: actions/upload-artifact@v3
        with:
          name: target
          path: target/release/
```
**Android / Gradle**
```yaml
jobs:
  build:
    runs-on: [ self-hosted, linux, customer-A ]
    steps:
      - uses: actions/checkout@v3
      - name: Setup JDK
        uses: actions/setup-java@v3
        with:
          java-version: '17'
      - name: Build APK
        run: ./gradlew assembleRelease
      - name: Upload APK
        uses: actions/upload-artifact@v3
        with:
          name: apk
          path: app/build/outputs/apk/release/
```
## 🛡️ Security & Isolation

- Each customer gets their own VM or ephemeral runner.
- Workspaces are deleted after each job.
- Outbound access is restricted to necessary endpoints (GitHub/GitLab, NPM registry, etc.)
- No SSH or direct access to the VM.

## 🏁 Getting Started

- Contact us to get your runner registration token.
- Add the runner to your GitHub/GitLab repository:
- Follow GitHub self-hosted runner guide
- Use the label provided in your workflow file (runs-on: [self-hosted, linux, customer-A]).
- Push code or trigger workflow_dispatch to start a build.

## 💰 Pricing & Payment

- Dedicated VM: €39 / month
- Optional shared pool (future, Best-Effort): €19 / month
- Payment methods: Bank Transfer or PayPal (fees included in PayPal).
- Invoice issued monthly.
- No SLA or uptime guarantee.
- Service is on a Best-Effort basis.

## 📜 License

- This repository is All Rights Reserved (no license).
- You may copy the example workflows for private use.
- If you want public reuse, we can add MIT license later.

## ⚠️ Notes

- Do not use for production-critical builds.
- Runner logs are visible on GitHub/GitLab but do not expose other customers’ data.
- Any issues with builds are resolved on a best-effort basis.
