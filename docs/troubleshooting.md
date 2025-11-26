# Troubleshooting

Common issues and resolutions for the **SIEM Platform**.

## Deployment Issues

### 1. Terraform State Lock

**Symptom:** `Error acquiring the state lock`

**Resolution:**
- Check if another deployment is running
- Verify DynamoDB lock table accessibility
- Force unlock if stuck: `terraform force-unlock <LOCK_ID>`

### 2. Cross-Account Access Denied

**Symptom:** Log sources can't write to central SIEM.

**Resolution:**
- Verify IAM role trust relationships
- Check resource-based policies on Kinesis streams
- Ensure organization ID is correct in policies

## Log Ingestion Issues

### 3. Missing Logs from Source

**Symptom:** Logs not appearing from specific account or service.

**Resolution:**
- Check CloudWatch Log subscription filter
- Verify Kinesis cross-account permissions
- Review Lambda processor errors
- Check log format matches parser configuration

### 4. High Log Processing Latency

**Symptom:** Logs delayed by minutes/hours.

**Resolution:**
- Check Kinesis shard utilization – add shards if needed
- Review Lambda concurrent executions – increase limits
- Check OpenSearch indexing rate – scale cluster

## Detection Issues

### 5. Too Many False Positives

**Symptom:** Alert fatigue from noisy detection rules.

**Resolution:**
- Tune detection thresholds based on baseline
- Add exception lists for known-good activity
- Implement alert deduplication rules

### 6. Missed Detections

**Symptom:** Known incidents not triggering alerts.

**Resolution:**
- Review detection rule coverage
- Check log source completeness
- Verify correlation rules are active
- Test with simulated attack data

## Performance Issues

### 7. Slow Dashboard Queries

**Symptom:** OpenSearch queries timing out.

**Resolution:**
- Add date range filters to queries
- Create summary indices for common queries
- Scale OpenSearch cluster (data nodes)
- Optimize index mappings

### 8. OpenSearch Cluster Red

**Symptom:** Cluster health shows red status.

**Resolution:**
- Check disk space on data nodes
- Review shard allocation issues
- Check for failed index operations
- Scale cluster or add storage

## Cost Issues

### 9. Unexpected High Costs

**Symptom:** Monthly bill higher than estimates.

**Resolution:**
- Review log ingestion volume by source
- Implement log filtering for verbose sources
- Check OpenSearch storage – enable lifecycle policies
- Review Kinesis shard count

> For architecture details, see `ARCHITECTURE.md`.
