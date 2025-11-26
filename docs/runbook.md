# Runbook

Operational guide for deploying, operating, and maintaining the **SIEM Platform**.

## 1. Deployment

### Prerequisites

- AWS CLI configured with appropriate credentials
- Terraform 1.5+ installed
- Access to target AWS accounts (security, log archive, workloads)

### Deploy Steps

```bash
# Initialize Terraform
terraform init

# Plan deployment (dev)
terraform plan -var="environment=dev" -out=tfplan

# Apply deployment
terraform apply tfplan

# For production
terraform plan -var="environment=prod" -out=tfplan
terraform apply tfplan
```

## 2. Log Source Onboarding

### Adding a New Log Source

1. Create log subscription in source account
2. Configure Kinesis cross-account access
3. Add log parser configuration
4. Test log flow end-to-end
5. Create detection rules for new source

### Common Log Sources

- CloudTrail (all accounts)
- VPC Flow Logs
- GuardDuty findings
- WAF logs
- Application logs

## 3. Monitoring

### Key Metrics to Watch

- **Log ingestion rate**: Kinesis incoming records
- **Processing latency**: Lambda duration metrics
- **OpenSearch health**: Cluster status, disk usage
- **Detection alerts**: Alert volume and false positive rate

### Dashboards

Pre-configured dashboards for:

- Security operations overview
- Threat detection summary
- Compliance status
- Log ingestion health

## 4. Incident Response

### Alert Triage Workflow

1. Review alert in SIEM dashboard
2. Correlate with related events
3. Investigate affected resources
4. Document findings
5. Escalate or close with resolution

### Forensics

```bash
# Export logs for investigation
aws s3 cp s3://siem-archives/2024/01/15/ ./investigation/ --recursive
```

## 5. Maintenance

### Regular Tasks

- Review and tune detection rules monthly
- Update threat intelligence feeds weekly
- Archive old logs per retention policy
- Patch OpenSearch cluster quarterly

### Teardown

```bash
terraform destroy -var="environment=dev"
```

> For troubleshooting common issues, see `docs/troubleshooting.md`.
