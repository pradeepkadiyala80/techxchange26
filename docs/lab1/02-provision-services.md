# 1.2 Provisioning Services

You will provision three IBM Cloud services that the Trade Finance application depends on.

---

## Services to Provision

| Service | Plan | Purpose |
|---------|------|---------|
| IBM Blockchain Platform | Starter | Smart contract execution |
| IBM Cloudant | Lite | Document storage |
| IBM API Connect | Lite | API gateway |

---

## Step 1 — Provision IBM Cloudant

```bash
ibmcloud resource service-instance-create trade-finance-db \
  cloudantnosqldb lite us-south \
  -p '{"legacyCredentials": false}'
```

Wait for the status to change to **active**:

```bash
ibmcloud resource service-instance trade-finance-db
```

---

## Step 2 — Create Cloudant Service Credentials

```bash
ibmcloud resource service-key-create trade-finance-db-creds \
  Manager \
  --instance-name trade-finance-db
```

Note down the `url` field from the output — you will use it in Lab 3.

---

## Step 3 — Provision IBM Blockchain Platform

```bash
ibmcloud resource service-instance-create trade-finance-blockchain \
  blockchain-platform standard us-south
```

> **Note:** Blockchain Platform provisioning can take 3–5 minutes.

Poll until active:

```bash
ibmcloud resource service-instance trade-finance-blockchain \
  --output json | grep '"state"'
```

---

## Step 4 — Verify All Services

```bash
ibmcloud resource service-instances \
  --service-name cloudantnosqldb
ibmcloud resource service-instances \
  --service-name blockchain-platform
```

Both should show `active` under the `State` column.

---

## ✅ Checkpoint

- [ ] Cloudant instance `trade-finance-db` is active
- [ ] Cloudant credentials created and `url` noted
- [ ] Blockchain Platform instance `trade-finance-blockchain` is active

---

*Next: [1.3 Configuring CLI Tools →](03-configure-cli.md)*
