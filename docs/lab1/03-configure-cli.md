# 1.3 Configuring CLI Tools

Configure your local environment so all tools point to the correct IBM Cloud region and services.

---

## Step 1 — Set Default Region

```bash
ibmcloud config --locale en_US
ibmcloud target -r us-south
```

---

## Step 2 — Clone the Lab Repository

```bash
git clone https://github.com/<your-org>/trade-finance-lab.git
cd trade-finance-lab
```

---

## Step 3 — Install Node Dependencies

```bash
npm install
```

Expected output ends with something similar to:

```
added 312 packages in 18s
```

---

## Step 4 — Configure Environment Variables

Copy the sample environment file:

```bash
cp .env.example .env
```

Open `.env` and fill in the values you collected in the previous section:

```bash
# .env
CLOUDANT_URL=https://<your-instance>.cloudantnosqldb.appdomain.cloud
CLOUDANT_APIKEY=<your-api-key>
BLOCKCHAIN_API_KEY=<your-blockchain-api-key>
APP_PORT=3000
```

---

## Step 5 — Smoke-Test the Configuration

```bash
npm run verify-config
```

Expected output:

```
✔ Cloudant connection successful
✔ Blockchain Platform reachable
✔ Configuration valid — ready to proceed
```

If any check fails, revisit the environment variable for that service.

---

## ✅ Checkpoint

- [ ] `npm install` completed without errors
- [ ] `.env` file populated with correct values
- [ ] `npm run verify-config` shows all green checkmarks

---

*Next: [Lab 2 — Letters of Credit →](../lab2/01-letters-of-credit.md)*
