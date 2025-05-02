Great! Based on your steps and request, here's an updated version of the article with your exact setup details included and a brief explanation comparing **GitHub-hosted** and **self-hosted** runners:

---

## 🚀 Setting Up a Self-Hosted GitHub Actions Runner on AWS EC2

For better performance, customization, and cost control, I decided to use a **self-hosted GitHub Actions runner** instead of relying on GitHub’s default hosted environment. Here's how I set it up on an **AWS EC2 instance**, step by step.

---

### 🤔 Why Self-Hosted?

GitHub offers two types of runners:

* **GitHub-hosted runners**: These are managed by GitHub. They're convenient—spinning up fresh VMs for each job—but limited in customization and may have cold start delays.
* **Self-hosted runners**: These run on your own machine or server (like an EC2 instance). You control the environment, can install custom tools, and often get faster build times.

---

### 🛠️ Step 1: Launch EC2 and Install Dependencies

I launched a basic Amazon Linux 2 EC2 instance.

Then I SSH'd into the instance and set up a working directory:

```bash
mkdir actions-runner && cd actions-runner
```

---

### 📦 Step 2: Download and Configure the Runner

I downloaded the runner package directly from GitHub:

```bash
curl -o actions-runner-linux-x64-2.323.0.tar.gz -L https://github.com/actions/runner/releases/download/v2.323.0/actions-runner-linux-x64-2.323.0.tar.gz
```

(You can optionally verify the file integrity with a SHA-256 hash.)

Then I extracted the contents:

```bash
tar xzf ./actions-runner-linux-x64-2.323.0.tar.gz
```

Next, I configured the runner by linking it to my GitHub repo:

```bash
./config.sh --url https://github.com/Hetpatel7131/GithubActions --token A7TZO4IJ6BI2VTUMEGVPA3DICVJXO
```

> Note: Use your own token here—GitHub provides a temporary one during setup.

Finally, I started the runner:

```bash
./run.sh
```

---

### 🔄 Step 3: Run the Runner as a Service

To keep the runner running in the background, even after reboot:

```bash
sudo ./svc.sh install
sudo ./svc.sh start
```

---

### ✅ The Result

Now, every time I push changes to my GitHub repo, GitHub Actions workflows trigger automatically on my EC2 instance. I can monitor job progress both on GitHub and directly on the instance.

This setup provides:

* Persistent runner that’s always available
* Faster build times (no container boot-up)
* Custom tool installation (e.g., Docker, Node, etc.)

---

### 🧪 Conclusion

Self-hosted runners are perfect if you need more flexibility and speed in your CI/CD process. Hosting one on AWS EC2 gave me full control over the build environment while still using GitHub Actions for orchestration.
