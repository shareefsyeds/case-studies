# Platform foundations

**Status:** live · **Role:** designed and built · **Setting:** internal platform at a clinical-trial technology company, 200+ users

**Interactive diagram:** [open it on the portfolio site](https://shareefsyeds.github.io/diagrams/platform.html). You can click each part, zoom and switch between light and dark.

The projects in the other write-ups sit on a platform that also does a lot of everyday work. This page covers that work in brief.

## Self-service apps

Eight apps that let staff run routine operations themselves. Every action is audited.

| App | What it does |
|---|---|
| Release automation | Validate and deploy software builds. The platform backs up first, copies and checksums each build, grants database roles and files the release documents. |
| Environment builds | Pick a configuration and pass a readiness check, then 21 automated steps handle database restore, app install, web server setup and single sign-on. |
| Self-service database accounts | Create, reset or lock your own account on up to 20 test databases at once, with production always out of reach. |
| Data provisioning with expiry | Request a dataset with a retention period. Schema, import and access are set up automatically, then removed when it expires. |
| Multi-tenant account management | Create, reset or change one account across every active customer environment in a single request. |
| Email deliverability checks | Find and clear suppressed email addresses directly in AWS. |
| Document delivery | Upload a document with a justification. It is archived and delivered into the downstream system automatically. |
| Operational dashboards | Dashboards and reports refreshed daily and weekly from the source systems. |

## Observability platform

Agent-based ingest, metrics, a log explorer, alert channels and runbook execution, with access set per project.

## Credential vault

Secrets with KMS envelope encryption, secret rotation, offline access, audit connectors and LDAP and Azure AD directory sync.

## Shared sign-in and AWS packages

Two internal Python and Django packages shared by several internal apps:

- Entra ID sign-in with JWT, API keys and role-based access control
- AWS connection management with credential rotation and audit

## From one VM to Amazon EKS

I designed the platform's AWS infrastructure in Terraform and Terragrunt and moved production from a single VM to Amazon EKS.

- EKS with Karpenter and Graviton nodes
- Aurora Serverless v2 and ElastiCache Valkey
- External Secrets with SSM
- Keyless GitHub OIDC deploys and VPC endpoints

## CloudWatch cost finding

I traced 91% of an AWS account's CloudWatch log-ingestion spend to one Lambda function logging at DEBUG level, a fix worth about $3K a month. I also built the case for a self-hosted log stack projected to save about $47.9K a year.
