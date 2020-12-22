# Edge Roadmap
This roadmap provides a guide of the current expectations for delivery. It is subject to change and will be regularly updated as priorities change and new requirements are confirmed.

## Complete the Replacement of Consul

Consul's role in the network is made up of two core requirements. Configuration store, and service health. We've had issues with Consul's ability to handle the hundreds of health checks currently active on network contributors so we will migrate this logic to Stargates. We'll also move configuration propagation to the gRPC service, and have both Gateway and Host receive config updates via a bidirectional stream.

## Replace Vault

Vault is currently used to handle ACL rules and device authentication, and works hand-in-hand with Consul. After completing the removal of Consul we'll need to migrate away from Vault entirely and use an authentication layer that combines in-memory bearer token distribution and user/pass login via the Network API.

## Auto Certificate Service

We've been auto-generating certificates for a while now using Let's Encrypt, but the way Let's Encrypt challenges the verification process has changed slightly. It now attempts the same challenge from a number of different geographic zones, meaning that the Gateway that the certificate request came from isn't necessarily going to be the only one that receives the challenge. To circumvent this issue, we're going to create a service that acts as a global cache for challenge keys and intermediary certificates, so that all Gateways have a single source of truth for the challenge assets. You can think of this as a network attached oracle for certifcates.

## Build Process

For the core network services we are moving away from Jenkins as a build service and replacing it with GitHub Actions. GitHub Actions are a fantastic and cost effective way to build for all the environments we currently support, and doesn't require us to maintain ageing ARM hardware which often comes with patchy support and unreliability issues that can cause all sorts of issues when trying to rapidly build and deploy hot fixes.

## Service Flushing and Staggered Deployment

There's a lot of resilience in the network, but a slow deploy can sometimes cause response delays and even timeouts. To avoid this, we're going to move away from a global deploy, and instead create a deployment queue that will see the Stargates and Gateways redirect traffic before updating. A key part of this change is in Stargate, which responds to BGP requests and Gateway DNS load balancing. Stargate will need to take itself out of the BGP group and wait for DNS requests to fall off before self updating and reconnecting. When Gateway is queued for update, it'll need to remove the Gateway from DNS resolution load balancing and confirm that the Gateway is receiving no traffic before it's allowed to self-update and rejoin.

## Edge Storage

Storage remains in alpha testing internally. It will be moved to a public beta and then in to production. The first production release will support small objects, < 2mb in size. This will be grown over time as we gather data about performance with real-world use cases and refine the platform.

Storage allows users to encrypt, store and retrieve files that are persisted in memory on the network. Files can be encrypted with your own keys, in much the same that crypto wallets are secured.

Individual files are broken in to hundreds of file fragments and split across multiple Network Nodes. This provides an incredibly secure solution for the storage of data.

We'll also be opening an API to directly access the storage services for beta testing.

## The Edge Site

While the [edge.network](http://edge.network) website recently received an update for the content delivery section, this is just a stop-gap solution on the way to a full website rebuild. The new site will be rebuilt in Vue, and will then be hooked up to an API for dynamic content. The focus of the site will be primarily on showcasing and selling content delivery, while keeping the technical network sections in less prominent locations. As we move through the year additional service areas will be added to the site. In addition to this tweaks to the brand will be made and a fresh lick of paint applied throughout.

We're an active business shifting from heavy R&D to a sales-led focus, so you can expect to see changes in this direction. This will include the opening up of a referral programme that will pay 10% of all revenue on service sales.

## Stake Automation

We will be providing smart contracts for the automation of staking within the network to enable the hands-off addition and removal of nodes from the network. This will be enabled alongside the reissue of the Edge token.

## Node Yields and Performance Scoring

The metrics used for the determining of payouts in the network will be evolving to more directly reward the completion of jobs whilst also recognising the length of service of nodes. Ultimately the network only really cares about the fast delivery of jobs from the job queue on Gateways. To this end nodes will be scored on the basis of the number of jobs that they have returned relative to their peer group on the Gateway that they are attached to. Alongside this we are exploring moving to a yield basis for rewards, with nodes earning an APR tied to their network score. This approach more fairly distributes rewards whilst giving preference those nodes that perform best for the jobs available within their Gateway. It is hoped that this change will help to keep contributed network hardware current whilst better incentivising those areas that require more capacity. Over time we hope to start to visualise this, enabling a more direct understanding of the average hardware in any given geographical area, along with a view of the rewards available.

## Console/Services Split

Currently Console handles both network contribution and service management. This will be split into two separate services (though with a single sign on): Console, and Services. The Services portal (services.edge.network) will be for management of network services such as Content Delivery, whereas Console will be restricted to network contribution only (e.g. Stakes, Devices, Earnings etc).

## Transition to PAYG Billing

We will be moving from subscription based billing to a pay as you go model. This will include a free buffer. This will require some reworking of Services (currently Console) and in API. There will be a monthly (or billing periodic) service that tallies up a customer's network usage and generates a single, itemised bill aggregating all service usage.

## Automated Crypto Payments

While payment in the Edge Network is possible in crypto today, automated payments are only enables in fiat. We will be providing a series of smart contracts for payment in crypto.

## Network Load & Monitoring

For a while we have had a simple network loading tool named Newton, which has been producing an artificial load on testnet. This has been super useful but we can do more. This service will be rewritten in Golang, will be configurable via Network API and will have a prometheus metrics interface for the reporting of data. Data reported will include metrics such as response time, response code, time-to-first-byte etc. This service will run externally from the network.

## Migration of Network Backbone to Data Centres

We are currently running the majority network backbone majority on rented hardware with providers around the world. We will be continuing the move to owned hardware with data centre parters. This will enable more fined-grained routing policies to better support inter-regional data transfers, which is especially useful for storage.

## DNS Interfaces

Edge DNS has been in production for over a year and has proven very stable and incredibly fast. We will be providing public interfaces for the use of this services, along with payment mechanisms and monitoring tools.

## Repackaging and Publishing Utilities

At present, a fair amount of the network code is contained in a private, monolithic "utils" package for convenience in development. However, as new tools are developed to support the network it becomes attractive to reorganise some of this code into individual packages to improve code confidence, robustness, and documentation. Additionally, further code can be open sourced. For example, the logger utility will be more usable across multiple products if repackaged individually. Repackaging work has already started and will continue through 2021 as emerging requirements dictate.
