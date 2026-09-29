# 5.1 Deploy to IBM Cloud

Package and deploy the Trade Finance application server to IBM Cloud Code Engine.

---

## Why Code Engine?

IBM Cloud Code Engine is a fully managed, serverless platform. It handles:
- Auto-scaling (including scale-to-zero)
- TLS termination and custom domains
- Container image builds directly from source

---

## Step 1 — Build the Container Image

```bash
ibmcloud ce project create --name trade-finance-lab
ibmcloud ce project select --name trade-finance-lab

ibmcloud ce buildrun submit \
  --name trade-finance-build \
  --source . \
  --strategy buildpacks \
  --image us.icr.io/<your-namespace>/trade-finance-app:latest
```

Wait for the build to complete:

```bash
ibmcloud ce buildrun get --name trade-finance-build
```

---

## Step 2 — Create a Secret for Environment Variables

```bash
ibmcloud ce secret create --name trade-finance-env \
  --from-env-file .env
```

---

## Step 3 — Deploy the Application

```bash
ibmcloud ce application create \
  --name trade-finance-app \
  --image us.icr.io/<your-namespace>/trade-finance-app:latest \
  --env-from-secret trade-finance-env \
  --port 3000 \
  --min-scale 1 \
  --max-scale 5
```

---

## Step 4 — Get the Application URL

```bash
ibmcloud ce application get \
  --name trade-finance-app \
  --output url
```

The URL will look like:
```
https://trade-finance-app.<region>.codeengine.appdomain.cloud
```

---

## Step 5 — Smoke-Test the Deployment

```bash
export APP_URL=$(ibmcloud ce application get \
  --name trade-finance-app --output url)

curl "$APP_URL/health"
# {"status":"ok","timestamp":"2026-..."}
```

---

## ✅ Checkpoint

- [ ] Container image built successfully
- [ ] Application deployed to Code Engine
- [ ] Health endpoint returns `{"status":"ok"}` from the public URL

---

*Next: [5.2 Monitor & Operate →](02-monitor.md)*
