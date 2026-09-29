# 3.3 Document Workflow

Implement the document submission and verification workflow that anchors document hashes on-chain.

---

## Overview

When a beneficiary submits shipping documents:
1. Documents are uploaded to **Cloudant** as attachments.
2. A **SHA-256 hash** of each document is computed.
3. The hash is **recorded on the blockchain** alongside the LC ID.
4. The issuing bank can verify document integrity at any time by recomputing the hash.

---

## Step 1 — Upload Document to Cloudant

```javascript
// src/services/documentService.js
const { CloudantV1 } = require('@ibm-cloud/cloudant');

const cloudant = CloudantV1.newInstance({ serviceName: 'TRADE_FINANCE_DB' });

async function uploadDocument(lcId, filename, buffer) {
    const docId = `${lcId}-${filename}`;
    // Create the document record
    await cloudant.putDocument({
        db: 'trade-documents',
        docId,
        document: { lcId, filename, uploadedAt: new Date().toISOString() }
    });
    // Attach the binary file
    await cloudant.putAttachment({
        db:         'trade-documents',
        docId,
        attachmentName: filename,
        attachment:     buffer,
        contentType:    'application/octet-stream'
    });
    return docId;
}
```

---

## Step 2 — Compute Document Hash

```javascript
const crypto = require('crypto');

function computeHash(buffer) {
    return 'sha256:' + crypto.createHash('sha256').update(buffer).digest('hex');
}
```

---

## Step 3 — Anchor Hash on Blockchain

```javascript
async function anchorDocumentHash(lcId, filename, hash, gateway) {
    const network  = await gateway.getNetwork('trade-channel');
    const contract = network.getContract('lc-contract');
    await contract.submitTransaction('presentDocuments', lcId, filename, hash);
}
```

---

## Step 4 — Submit Documents via API

```bash
curl -s -X POST http://localhost:3000/api/lc/LC-2026-0001/documents \
  -F "file=@/path/to/bill-of-lading.pdf" | jq .
```

Expected response:

```json
{
  "docId": "LC-2026-0001-bill-of-lading.pdf",
  "hash": "sha256:3b4c5d...",
  "txId": "m3n4o5p6...",
  "status": "DOCUMENTS_PRESENTED"
}
```

---

## Step 5 — Verify Document Integrity

```bash
curl -s http://localhost:3000/api/lc/LC-2026-0001/verify \
  -G --data-urlencode "filename=bill-of-lading.pdf" | jq .
```

Expected response:

```json
{
  "verified": true,
  "onChainHash": "sha256:3b4c5d...",
  "computedHash": "sha256:3b4c5d...",
  "match": true
}
```

---

## ✅ Checkpoint

- [ ] Document uploaded successfully to Cloudant
- [ ] Hash anchored on-chain (`txId` returned)
- [ ] Verification endpoint returns `"verified": true`

---

*Next: [Lab 4 — Unit Testing →](../lab4/01-unit-testing.md)*
