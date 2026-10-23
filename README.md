# dgcl-sec-devsecops-tools

A centralized, internal repository for storing and distributing DevSecOps tool executables and binaries used across DGCL engineering and security teams.

---

## 📦 What's in this repo?

This repository hosts versioned binaries and executables for the following categories of DevSecOps tools:

### 🔍 Static Application Security Testing (SAST)
- **Coverity Analysis** — Static code analysis tool by Black Duck (Synopsys) for identifying security vulnerabilities and code defects at the source level.

### 🧩 Software Composition Analysis (SCA)
- **Black Duck SCA** — Identifies open source components, licenses, and known vulnerabilities in your codebase and dependencies.

### 🕵️ Interactive Application Security Testing (IAST)
- **Seeker IAST** — Runtime security testing agents that monitor applications during testing to detect vulnerabilities through actual usage.

---

## 🗂️ Repository Structure

```
dgcl-sec-devsecops-tools/
├── coverity/               # Coverity Analysis binaries
├── blackduck/              # Black Duck SCA utilities
├── seeker/                 # Seeker IAST agents
└── README.md
```

> **Note:** Large binary files are stored using [Git LFS](https://git-lfs.github.com/). Ensure Git LFS is installed before cloning.

---

## 🚀 Getting Started

### Prerequisites

- Git installed
- [Git LFS](https://git-lfs.github.com/) installed:
  ```bash
  # Mac
  brew install git-lfs

  # Linux
  sudo apt-get install git-lfs

  # After installing
  git lfs install
  ```

### Clone the repository

```bash
git clone https://github.com/dgcl-cloud/dgcl-sec-devsecops-tools.git
cd dgcl-sec-devsecops-tools
```

Git LFS will automatically pull the binary files during clone.

---

## 📋 Supported Platforms

| Tool | Windows | macOS (Intel) | macOS (ARM) | Linux (x64) |
|------|---------|--------------|-------------|-------------|
| Coverity Analysis | ✅ | ✅ | ✅ | ✅ |
| Black Duck SCA | ✅ | ✅ | ✅ | ✅ |
| Seeker IAST Agent | ✅ | ✅ | ✅ | ✅ |

---

## 🔐 Access & Usage

This is a **private, internal repository** intended for use by the **DGCL Security and DevSecOps team only**.

- Do not share credentials or repository access externally.
- All tools in this repository are licensed software — refer to [`LICENSE.md`](./LICENSE.md) for terms.
- For access requests, contact the DevSecOps team.

---

## 🛠️ Contributing

To add a new tool version or binary:

1. Clone the repo and ensure Git LFS is set up.
2. Place the binary in the appropriate tool subfolder.
3. Run:
   ```bash
   git add .
   git commit -m "Add <tool-name> v<version> for <platform>"
   git push origin main
   ```

Please follow the naming convention:
```
<tool-name>-<os>-<version>.<ext>
# Example: cov-analysis-linux64-2026.3.0.tar.gz
```

---

## 📞 Contact

For questions or access issues, reach out to the **DGCL DevSecOps Team** via your internal communication channels.
