# Prerequisites

Before you begin the labs, ensure the following tools and access are in place.

---

## Required Accounts

| Account | Notes |
|---------|-------|
| **IBM Cloud** | Free Lite account is sufficient. [Sign up →](https://cloud.ibm.com/registration) |
| **GitHub** | Required to fork the lab repo. [Sign up →](https://github.com/join) |

---

## Required Tools

Install all tools before Lab 1. Run the verification commands to confirm each is installed correctly.

### Node.js (v18 LTS or higher)

```bash
node --version   # expected: v18.x.x or higher
npm --version    # expected: 9.x.x or higher
```

[Download Node.js →](https://nodejs.org)

### IBM Cloud CLI

```bash
ibmcloud version   # expected: ibmcloud version 2.x.x
```

```bash
# Install (macOS / Linux)
curl -fsSL https://clis.cloud.ibm.com/install/linux | sh

# Install (Windows PowerShell — run as Administrator)
iex (New-Object Net.WebClient).DownloadString('https://clis.cloud.ibm.com/install/powershell')
```

### Git

```bash
git --version   # expected: git version 2.x.x
```

### Docker (optional — for local chaincode development)

```bash
docker --version   # expected: Docker version 24.x.x
```

---

## Verify Everything at Once

Run this one-liner to check all prerequisites simultaneously:

```bash
node --version && npm --version && git --version && ibmcloud version
```

All four lines should print version numbers without errors. If any command fails, install the missing tool using the link above before continuing.

---

*Next: [Architecture Overview →](architecture.md)*
