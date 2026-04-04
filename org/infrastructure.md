# Infrastructure Decision Record

> Fill this out when adopting the framework for your organization.
> This becomes the agent's understanding of your technical environment.

## Source Control

- **Platform:** [GitHub / GitLab / Bitbucket / Azure DevOps / Gitea]
- **Branching strategy:** [GitHub Flow / GitFlow / Trunk-Based]
- **Default branch:** [main / master]
- **Branch protection rules:**
  - Required approvals: [number]
  - Required CI checks: [list]
  - Enforce linear history: [yes/no]
- **Merge method:** [Squash / Rebase / Merge commit]

## Development Environment

- **Standard setup:** [Native / Dev Container / Cloud IDE]
- **Required tools:**
  - [Tool 1] version [X]
  - [Tool 2] version [X]
- **Setup automation:** [script name or Makefile target]
- **IDE:** [VS Code / JetBrains / Neovim / other]
- **IDE extensions:** [required extensions]

## Languages and Frameworks

- **Primary language(s):** [Python / TypeScript / Java / Rust / Go / etc.]
- **Framework(s):** [FastAPI / Django / Spring / etc.]
- **Package manager:** [pip / npm / maven / cargo / etc.]
- **Linting:** [tool and config]
- **Formatting:** [tool and config]
- **Type checking:** [tool and config]

## Runtime and Deployment

- **Primary deployment target:** [K8s / ECS / Bare-metal / Serverless / VM]
- **Container registry:** [ECR / GCR / Docker Hub / self-hosted / N/A]
- **Performance-critical components:** [Container / Bare-metal / GPU]
- **Service mesh:** [Istio / Linkerd / None]
- **Configuration management:** [Ansible / Terraform / Pulumi / CloudFormation]

## CI/CD

- **CI platform:** [GitHub Actions / GitLab CI / Jenkins / CircleCI / Buildkite]
- **Deployment strategy:** [Blue-Green / Canary / Rolling / GitOps]
- **Required CI gates:**
  - [ ] Unit tests
  - [ ] Integration tests
  - [ ] Linting
  - [ ] Security scan
  - [ ] Domain-specific evaluation
- **Deployment pipeline:** [describe stages]

## Observability

- **Logging:** [ELK / Loki / Datadog / CloudWatch / Splunk]
- **Metrics:** [Prometheus / Datadog / CloudWatch / New Relic]
- **Tracing:** [Jaeger / Zipkin / Datadog / X-Ray]
- **Alerting:** [PagerDuty / OpsGenie / Slack / email]
- **Key dashboards:** [list with URLs]

## Workflow Tools

- **Issue tracking:** [Jira / Linear / GitHub Issues / GitLab Issues]
- **Documentation:** [Confluence / Notion / Markdown / GitBook]
- **Communication:** [Slack / Teams / Discord]
- **Project tracking URL:** [URL]
- **Documentation URL:** [URL]

## Data Infrastructure

- **Data warehouse:** [BigQuery / Snowflake / Redshift / Databricks / ClickHouse]
- **Search engine:** [Elasticsearch / OpenSearch / Solr / Vespa / custom]
- **Cache:** [Redis / Memcached / none]
- **Message queue:** [Kafka / RabbitMQ / SQS / Pub/Sub / none]
- **Object storage:** [S3 / GCS / Azure Blob / MinIO]

## AI Tools

- **Approved AI tools:** [list]
- **Data governance restrictions:** [what cannot be sent to AI APIs]
- **API access method:** [direct / proxy / VPN / self-hosted]
- **Self-hosted models (if any):** [model names and serving platform]

## Network and Security

- **Network access:** [cloud VPC / on-prem / hybrid / air-gapped]
- **Authentication:** [SSO provider / method]
- **Secret management:** [Vault / AWS Secrets Manager / GCP Secret Manager / etc.]
- **Compliance requirements:** [SOC2 / HIPAA / GDPR / PCI / FedRAMP / none]
