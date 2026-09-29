# 5.2 Monitor & Operate

Use IBM Cloud Monitoring and Log Analysis to observe your running Trade Finance application.

---

## Accessing Logs

### Real-Time Logs via CLI

```bash
ibmcloud ce application logs \
  --name trade-finance-app \
  --follow
```

Press `Ctrl+C` to stop streaming.

---

### IBM Log Analysis

1. Open the [IBM Cloud Observability dashboard](https://cloud.ibm.com/observe/logging).
2. Select your **Log Analysis** instance.
3. In the search bar, type `trade-finance-app` to filter logs.

---

## Key Metrics to Watch

| Metric | Normal Range | Action if Exceeded |
|--------|-------------|-------------------|
| CPU usage | < 70% | Scale up (`--max-scale`) |
| Memory usage | < 80% | Increase instance memory |
| HTTP error rate (5xx) | < 1% | Review application logs |
| Transaction latency (p95) | < 2 s | Check blockchain network health |

---

## Setting Up Alerts

```bash
# Install Monitoring plugin if not already installed
ibmcloud plugin install monitoring

# Create a CPU alert
ibmcloud monitoring alert create \
  --name high-cpu \
  --metric cpu.used.percent \
  --threshold 80 \
  --duration 5m \
  --notify email:<your-email>
```

---

## Scaling the Application

Scale out to handle load:

```bash
ibmcloud ce application update \
  --name trade-finance-app \
  --min-scale 2 \
  --max-scale 10
```

---

## ✅ Checkpoint

- [ ] Real-time logs are streaming without errors
- [ ] IBM Log Analysis shows application log entries
- [ ] At least one alert rule configured

---

*Next: [Summary & Next Steps →](../wrapup/summary.md)*
