# Cost Analysis (₹)

This document provides cost estimates for the **SIEM Platform** architecture in **Indian Rupees (₹)**.

## Production Environment

At production scale (enterprise-wide log collection), the architecture typically costs:

| Service | Monthly Cost (₹) | Notes |
|---------|------------------|-------|
| **Security Lake** | ₹30,000–50,000 | Centralized log storage |
| **OpenSearch** | ₹60,000–100,000 | Log analytics and SIEM dashboards |
| **Kinesis Data Streams** | ₹15,000–25,000 | Real-time log ingestion |
| **Lambda (processors)** | ₹10,000–20,000 | Log transformation and correlation |
| **GuardDuty** | ₹25,000–40,000 | Threat detection |
| **Security Hub** | ₹5,000–10,000 | Compliance aggregation |
| **S3 (archives)** | ₹8,000–15,000 | Long-term log retention |
| **Total** | **₹150,000–260,000** | ~$1,875–3,250/month |

## Development Environment

For dev/staging environments:

| Environment | Approx Monthly Cost (₹) | Notes |
|------------|--------------------------|-------|
| Dev | ₹25,000–40,000 | Single account, reduced log volume |
| Staging | ₹60,000–100,000 | Multi-account, test data |
| Production | ₹150,000–260,000 | Enterprise-wide, full retention |

## Cost Optimization Strategies

- **Log filtering** – Filter verbose logs at source before ingestion
- **Tiered storage** – Move older logs to S3 Glacier after 90 days
- **Reserved instances** – Use reserved pricing for OpenSearch
- **Sampling** – Sample high-volume, low-value log sources
- **Retention policies** – Align retention with compliance requirements

## Related Documentation

See `ARCHITECTURE.md` for service details and `DEPLOYMENT.md` for configuration options.
