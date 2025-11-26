# Security Overview

This document summarizes the security posture of the **SIEM Platform** architecture.

## Defense-in-Depth

The SIEM platform itself must be highly secured as it processes sensitive security data.

### Identity & Access (IAM)

- Least-privilege IAM roles for all SIEM components
- Separate roles for log ingestion, processing, and analyst access
- MFA required for analyst console access
- Break-glass procedures for emergency access

### Data Protection

- **At rest**: KMS encryption with customer-managed keys for all log storage
- **In transit**: TLS 1.3 for all log transport and API calls
- **Key rotation**: Automated KMS key rotation enabled
- **Data classification**: Logs tagged by sensitivity level

### Network Isolation

- OpenSearch deployed in private VPC subnets
- VPC endpoints for all AWS service access
- No public internet access for data plane components
- WAF protection for analyst dashboards

### Access Controls

- Role-based access control (RBAC) for analyst dashboards
- Attribute-based access for multi-tenant scenarios
- Session recording for privileged access
- Audit logging of all analyst queries

## Threat Intelligence Integration

- Automated IOC feeds ingestion
- Threat intel correlation with log data
- Automated blocking rules for known threats

## Compliance

The architecture supports:

- SOC 2 Type II audit requirements
- PCI-DSS logging requirements
- HIPAA audit logging
- GDPR data protection controls

> For detailed security configurations, see `SECURITY.md` in the project root.
