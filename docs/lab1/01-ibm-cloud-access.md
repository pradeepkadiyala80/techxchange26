# 1.1 Accessing IBM Cloud

In this section you will log in to IBM Cloud and verify that your account is ready for the lab.

---

## Step 1 — Log in via CLI

```bash
ibmcloud login --sso
```

> **Tip:** The `--sso` flag lets you authenticate using a one-time passcode from your browser — no need to type your password.

Follow the prompts:
1. A URL will be printed. Open it in your browser.
2. Copy the one-time passcode.
3. Paste it back in the terminal and press **Enter**.

---

## Step 2 — Target a Resource Group

```bash
ibmcloud target -g Default
```

Expected output:

```
Targeted resource group Default
```

---

## Step 3 — Verify Your Account

```bash
ibmcloud account show
```

Confirm that:
- Your account name appears correctly.
- The account type is **Pay-As-You-Go** or **Lite**.

---

## Step 4 — Install Required CLI Plugins

```bash
ibmcloud plugin install blockchain
ibmcloud plugin install cloud-databases
```

Verify plugins are installed:

```bash
ibmcloud plugin list
```

You should see `blockchain` and `cloud-databases` in the list.

---

## ✅ Checkpoint

Before moving to the next section, confirm:

- [ ] `ibmcloud login` succeeded without errors
- [ ] Resource group `Default` is targeted
- [ ] Both CLI plugins are listed

---

*Next: [1.2 Provisioning Services →](02-provision-services.md)*
