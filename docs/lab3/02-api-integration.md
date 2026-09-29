# 3.2 API Integration

Connect the Node.js application server to both the IBM Blockchain Platform and Cloudant.

---

## Step 1 — Fabric SDK Gateway Setup

The application uses the **Hyperledger Fabric Node SDK** to connect to the blockchain network.

```javascript
// src/fabric/gateway.js
const { Gateway, Wallets } = require('fabric-network');
const path = require('path');
const fs   = require('fs');

async function getGateway() {
    const ccpPath = path.resolve(__dirname, '..', 'connection-profile.json');
    const ccp     = JSON.parse(fs.readFileSync(ccpPath, 'utf8'));

    const walletPath = path.join(__dirname, '..', 'wallet');
    const wallet     = await Wallets.newFileSystemWallet(walletPath);

    const gateway = new Gateway();
    await gateway.connect(ccp, {
        wallet,
        identity: 'appUser',
        discovery: { enabled: true, asLocalhost: false }
    });

    return gateway;
}

module.exports = { getGateway };
```

---

## Step 2 — Enrol Application User

Before the server can submit transactions, it needs an enrolled identity in the wallet:

```bash
node scripts/enrollUser.js
```

Expected output:

```
✔ Admin enrolled
✔ Application user "appUser" enrolled and stored in wallet
```

---

## Step 3 — LC API Route

```javascript
// src/routes/lc.js
const express = require('express');
const router  = express.Router();
const { getGateway } = require('../fabric/gateway');

router.post('/apply', async (req, res) => {
    const { applicant, beneficiary, amount, currency, expiryDate, goods } = req.body;
    const gateway = await getGateway();
    try {
        const network  = await gateway.getNetwork('trade-channel');
        const contract = network.getContract('lc-contract');
        const result   = await contract.submitTransaction(
            'applyLC', applicant, beneficiary,
            String(amount), currency, expiryDate, goods
        );
        res.json(JSON.parse(result.toString()));
    } finally {
        gateway.disconnect();
    }
});

module.exports = router;
```

---

## Step 4 — Start the Application Server

```bash
npm start
```

The server starts on port `3000` (or the value of `APP_PORT` in `.env`).

Test the health endpoint:

```bash
curl http://localhost:3000/health
# {"status":"ok","timestamp":"2026-..."}
```

---

## ✅ Checkpoint

- [ ] `enrollUser.js` completed without errors
- [ ] Application server starts on port 3000
- [ ] `/health` endpoint returns `{"status":"ok"}`

---

*Next: [3.3 Document Workflow →](03-document-workflow.md)*
