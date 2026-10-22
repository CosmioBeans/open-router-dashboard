# Feature catalog

Status: agreed product direction with proposed implementation detail, recorded October 20, 2026; reviewed October 22, 2026. All features are unimplemented. This is a growing scope catalog, not a first-release commitment or a hardware support claim.

The [navigation document](navigation.md) owns page placement. The [scenario matrix](scenarios.md) defines where features apply. This document owns behavior and shared requirements.

## Status and identifiers

- **Planned direction:** the feature families and principles accepted in discussion. Exact controls, backend choices, and release placement remain open.
- **Candidate:** an earlier brainstorming idea that still needs an explicit scope decision.
- **Implemented/tested:** not applicable to any entry yet. Future claims need linked implementation and validation evidence.

Stable feature IDs below support later issues and specifications. Keep an ID when its wording changes; do not reuse retired IDs for unrelated features. Proposed details describe how to refine an agreed family without claiming that every mechanism is already decided.

## Overview and devices

| ID | Planned direction | Scope and constraints |
| --- | --- | --- |
| F01 | Customizable overview | Connectivity, alerts, versions, service health, selected metrics, and shortcuts. Reorder/hide widgets and restore defaults. |
| F02 | Device inventory | Active/recent clients, names, notes, labels, addresses, connection type, AP/port association, last seen, and history where observable. Device identification must show uncertainty. |
| F03 | Device groups and assignments | Reusable groups and profiles; assign access, filtering, bandwidth, and VPN policies. Reservation and policy actions use the owning feature's shared editor. |

## Network

| ID | Planned direction | Scope and constraints |
| --- | --- | --- |
| F04 | Setup and topology | Composable roles, guided presets, upstream/downstream relationships, and ownership of routing, DHCP, DNS, and filtering. Separate managed, discovered, and manually described equipment; label inferred relationships. |
| F05 | Internet connections | Dynamic/static addressing, PPPoE where supported, ISP VLAN requirements, IPv6, MTU, DNS overrides, wired/wireless/cellular uplinks, and status. Preserve the distinction between an uplink and local access Wi-Fi. |
| F06 | Multiple uplinks | Failover, load balancing, health checks, and policy-specific behavior. Explain connection changes, DNS/VPN effects, and reachability limits. Distinguish load balancing from connection bonding; document interruption and reconnection behavior for established sessions during failover. |
| F07 | Local networks | Subnets, network membership, bridges, guest/IoT separation, IPv4/IPv6, and per-network configuration. Link isolation and discovery rules to their shared owners. |
| F08 | Ports and switching | Port roles, link status, tagged/untagged VLAN membership, bridges, and transport across supported uplinks/backhaul. |
| F09 | DHCP and reservations | Pools, leases, reservations, DHCP options, DHCPv6, and router advertisements where appropriate. Identify external service ownership and avoid conflicting servers. |
| F10 | DNS | Upstream resolvers, local records, forwarding/split DNS, encrypted upstream options, and diagnostics. Coordinate resolver ownership with filtering modules. |
| F11 | Routing | Static routes and policy routing, with dynamic routing as an optional integration. IPv4/IPv6 and VPN views share authoritative objects. |
| F12 | Bandwidth and prioritization | SQM/queue management, priorities, bandwidth limits, and compatible offload controls. Explain dependencies and measure shaping/accounting/offload combinations before support claims. |

## Wi-Fi

| ID | Planned direction | Scope and constraints |
| --- | --- | --- |
| F13 | Wireless networks | SSIDs, security/passwords, QR sharing, guest networks, network assignments, isolation, and schedules. Reuse policies rather than create competing configuration. |
| F14 | Radios and channels | Bands, channels, widths, power, country settings, surveys, and supported standards. Distinguish hardware support, configured settings, and client-negotiated capabilities. |
| F15 | Access points and mesh | Node inventory, wired/wireless backhaul, neighbors, paths, roaming coordination, and compatible shared settings. Central management requires enrollment and authenticated access; visible third-party equipment is not automatically manageable. |

## VPN

| ID | Planned direction | Scope and constraints |
| --- | --- | --- |
| F16 | VPN clients | Outbound profiles, imports, authentication/keys, connection controls, status, routing/DNS, reconnect behavior, and logs. |
| F17 | VPN servers | Hosted servers, protocol-appropriate users/peers, connection profile export, network access, sessions, and logs. Peers stay associated with their server/tunnel. |
| F18 | Site-to-site and overlays | Connections between networks and optional overlay integrations. Represent shared tunnel objects once; protocol and provider choices remain open. |
| F19 | VPN routing policies | Device/network assignments, exclusions, split tunneling, and explicit behavior when a tunnel fails. Integrate with shared policy routing and prevent unexplained fallback. |

## Security

| ID | Planned direction | Scope and constraints |
| --- | --- | --- |
| F20 | Firewall | Zones, traffic rules, inter-network permissions, IPv4/IPv6 consistency, validation, and readable effective behavior. |
| F21 | Port forwarding | Mappings, optional expiry, conflicts, and diagnostics for upstream restrictions. A local rule does not prove internet reachability. |
| F22 | Access policies | Device/network restrictions, pauses, reusable schedules/profiles, and understandable exceptions. Apply only where this device can enforce them. |
| F23 | Ad blocking and filtering | Enable/pause, blocklists and update status, allowlists, custom rules, matching-rule explanations, exceptions, and backend-supported device/network profiles. Optional query history must have retention controls. |
| F24 | Guest portal | Admission and session controls for supported guest deployments. Hosting a portal is distinct from signing in to an upstream travel-network portal. |
| F25 | Automatic port mapping | Supported automatic mapping controls and visibility of active mappings. Explain exposure and conflicts with manually configured rules. |

### Filtering behavior

Use a supported backend behind a consistent interface; backend selection remains open. Prevent competing resolver configurations. Verify whether intended clients use the filtering resolver and explain bypass paths or missing visibility.

Count blocked DNS queries accurately; do not call them ads removed or threats prevented. DNS-based filtering cannot selectively remove ads that share a domain with wanted content. See [OpenWrt ad-blocking options](https://openwrt.org/docs/guide-user/services/ad-blocking) and the [AdGuard Home FAQ](https://github.com/AdguardTeam/AdGuardHome/wiki/FAQ).

## Services

| ID | Planned direction | Scope and constraints |
| --- | --- | --- |
| F26 | Dynamic DNS | Provider profiles, update state, detected address, and useful failure messages. An updated record does not remove upstream NAT restrictions. |
| F27 | File and printer sharing | Optional hosted services with access controls, status, and storage/device dependencies. Filesystem/device administration belongs under System. |
| F28 | Additional service integrations | Named pages for explicitly integrated services; shared module dependencies and resource budgets. Raw package availability does not promise a custom UI. |

## Monitoring

| ID | Planned direction | Scope and constraints |
| --- | --- | --- |
| F29 | Traffic and usage | Live/historical traffic, per-device/interface totals, comparisons, and export where collection is reliable. Explain missing paths and possible double counting across observation points. |
| F30 | Connection quality | Uplink availability, latency, jitter, loss, reconnects, failover events, and observable wireless/backhaul quality. Label active probes and test overhead. |
| F31 | Router health | CPU, memory, storage, temperature where exposed, interface counters/errors, and service health. |
| F32 | Events and logs | System/service logs, configuration and connection events, filtering explanations, and a shared timeline. Correlation is not proof of cause. |
| F33 | Diagnostic tools | Ping, route tracing, DNS tests, wireless diagnostics, connection inspection, and scoped packet capture. Provide sanitized support export and clear tool permissions. |

### Measurement contract

Each measurement should declare scope, source, units, timestamp/freshness, sampling interval, and retention. Distinguish unavailable, unknown, stale, and zero. Identify measured versus inferred values and gaps in collection.

Keep negotiated link rates distinct from measured throughput. Device identity and topology discovery can be incomplete. A gateway cannot assume visibility into all switched or third-party traffic; an AP cannot assume visibility into every client in the building. See the scenario matrix for these boundaries.

Detailed history is configurable: retention, collection frequency, local storage limits, export, and optional remote collection. Plan for bounded flash writes, CPU/RAM use, and safe handling of full storage. Sensitive query or traffic histories require explicit enablement and deletion controls. Hardware acceleration and collection methods need compatibility tests.

## System

| ID | Planned direction | Scope and constraints |
| --- | --- | --- |
| F34 | Updates | Distinct firmware/dashboard/module releases, release notes, compatibility checks, authenticated metadata, artifact verification, progress, and post-install checks. GitHub hosts versioned artifacts; an updater must still be implemented. |
| F35 | Software and modules | Discover, install, remove, and inspect compatible integrations and dependencies. Explain resource needs, conflicts, and schema compatibility; installation does not choose policy automatically. |
| F36 | Backups and recovery | Configuration export/import, protection, verification, compatibility, change previews, and applicable timed reversion. Configuration restoration, UI rollback, and firmware recovery are different operations. |
| F37 | Administration | Accounts/roles, credentials, sessions, web/SSH access, keys, certificates, and auditability. Identity/permission architecture is an open implementation decision. |
| F38 | Hardware, time, and region | Supported hardware controls, storage/USB information, hostname, time synchronization, regional/language preferences, and accessible presentation. Radio regulatory settings remain with Radios & Channels. |
| F39 | Automation and service management | Reusable schedules, explicit maintenance actions, and advanced service runtime/startup controls. Wi-Fi/access schedules reference shared objects; service settings remain on their feature page. |
| F40 | Reboot and reset | Clear scope, expected interruption, confirmation, and reconnection/recovery guidance. |

## Installation workflow

The desktop installer is a separate delivery surface, not another sidebar section. Planned direction includes compatibility inspection, authenticated router access, an off-device backup, verified target-specific artifacts, a concrete pre-install review, supported installation procedures, and reconnection checks. A dashboard package install and a firmware migration are different operations. Host platforms, migration paths, and automation limits remain undecided.

## Shared product behavior

- Shared capability discovery evaluates hardware, drivers, installed software, role, permissions, and runtime health. Backend checks enforce the same restrictions as the interface.
- One authoritative object/editor per setting or policy; context views reuse it. Define precedence per policy family and show effective values, defaults, and overrides.
- Search, favorites, reusable help, accessible controls, validation, and useful error messages follow the navigation contract.
- Local administration works without internet access. Updates and external integrations show their own unavailable state.
- Consequential changes preview affected objects and interruption; recovery behavior must be defined and tested before claims are made.
- Modularity includes shared behavior and clean interfaces, not just reusable visual components. Hardware exceptions stay in isolated adapters rather than scattered model-name checks.

## Candidates retained for discussion

These ideas from earlier brainstorming remain candidates rather than agreed release scope: data quotas; configurable external notifications; link aggregation; multi-link wireless operation; advanced multicast/service-discovery controls; external metrics and remote logging integrations; a public API/CLI; offline installation bundles; scheduled encrypted backups; staged fleet updates; and portable configuration profiles. Some are natural extensions of planned families, but each needs a concrete design and capability assessment.

## Feature refinement checklist

Before implementation, add detail beside the owning entry or link a focused specification when needed: purpose; canonical home; controls and help; capabilities and dependencies; permissions; shared objects and precedence; applicable scenario IDs; collection/storage costs; failure and recovery behavior; migration requirements; acceptance checks; and open decisions. Assign a release only after scope is agreed.
