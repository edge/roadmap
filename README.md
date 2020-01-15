# Edge Roadmap
This roadmap provides a guide of the current expectations for delivery. It is subject to change and will be regularly updated as priorities change and new requirements are confirmed.

## Q1

### Consul KV Migration
Migration from using Consul to store network configurations to an RPC method. This will reduce load on the network, reduce latency between Stargate boot and config propagation, and reduce the number of open ports on Stargate.

### API 6 Migration
Migrating the API 6.x makes it possible to offer application tokens in preperation for an Edge CLI upgrade which will see users only required to log in once.

### Stake watch service
As part of a two-phase approach to onboarding automation, a process will be built to initially monitor a wallet but eventually a contract to determine the status of a device stake.

### DB data backup
As part of a routine improvement plan for network resilience, databases are to be backed up to multiple sites.

### Migrate all internal services to managed deployment
An improvement to the deployment process introducing automation.

### Persist Gateway requests and data transfer per domain
Increasing the accuracy of usage calculations by persisting the data transfer and request count through Gateway from telemetry.

### Console
Rebuild of the existing my.edge.network UI as a webapp.

### Telemetry for request and payload data
Gathering various data points through the use of a secure Prometheus endpoint.

### Stake transfer (CLI only)
CLI to allow the transfer of stake and the selection of available stake during the onboarding process.

### Migrate data to new platform
Migrating disk stored data to the new containered platform.

### Launch new Console + rollout of API 6.X support
Testing and deployment of the new webapp Console.

### Redirect API requests to new API server (post-API 6.x release)
Redirect service as part of the migration from legacy API to API 6.x

### Disk cache
Enhancing the cache by adopting a disk cache to support the existing memory cache.

### CDN Gif support
GIF resizing support in CDN.

## Q2

### DNS zone support
Support for zones to remove the potential for conflicting DNS records after ownership change.

### Migrate all internal services to managed deployment — Phase 2
Further tasks to complete the migration to a fully managed deployment stack.

### Remote logging capture (core services only)
Remote logging for all core services to improve disk performance and mitigate the potential for disk availability errors.

### Alerts for all critical warnings
Critical warnings to be part of an alerting service for core team.

### Sync build digests with API for Agent, Host and CDN
Build digests to be persisted in the core database automatically after build.

### Billing calculation based on Persist Gateway requests and data transfer per domain
Billing service to calculate accurate usage using Gateway telemetry on a per domain basis.

### Console Payments
Payment platform to accept fiat payments and conversion to $EDGE through the new console.

### Exposed public API for third party integration. 
Public API to expose device data. Limited, but with optional high limit user keys on request.

### CDN use GRPC for config
CDN to be configured via encrypted RPC request.

### CDN use key instead of domain
Requests to CDN to be made with an app key rather than a domain as a security measure.

### CDN device benchmarking on launch
Devices to benchmark CDN on boot to establish a device scoring.

### CLI MacOS support
CLI to support MacOS.

### Migrate Services away from Consul
Services to be indexed outside of Consul.

### Storage Beta release
Storage to offer non-persisted limited beta for first phase of distribution tests.

## Q3

### DNS in Console
Interface for creation and editing of DNS zones and records.

### CLI Watch service
A command line interface visualiser of device telemetry.

### Storage persisted
Persist storage data after device redeployment.

### Store DNS usage
Capture and store DNS telemetry from Stargate.

### Telemetry on Agent
Improve telemetry and re-introduce proxy service for Agent.

### Telemetry on Host
Improve telemetry and re-introduce proxy service for Host.

### Payouts based on Host usage
Accurate payment mechanism to include uptime as well as network traffic and request counts.

