# Feature catalog

Status: candidates for discussion. No item in this catalog has been approved for implementation, assigned a release, or declared supported. The list will grow as we discuss the project.

These groups describe functional ownership, not a final navigation layout. Each future feature should have one primary home; other screens can reference it without duplicating its settings.

## System overview

Internet and local-network health; interface status; uptime; firmware and dashboard versions; CPU, memory, storage, and temperature where exposed; active alerts; recent configuration changes; service health; a summary of detected capabilities.

## Devices

Connected and recently seen clients; names and labels; IPv4/IPv6 addresses; connection type; radio/access point association; signal and negotiated link rates; device groups; DHCP reservations; access schedules; temporary blocking; traffic summaries; new-device notifications. Identification should expose uncertainty rather than invent a device type.

## Internet connections

Dynamic and static addressing; PPPoE; ISP VLAN requirements; DNS; IPv6 provisioning and prefix delegation; MTU; MAC override where supported; connection tests; multiple WANs; failover; load balancing; cellular/USB tethering; data limits; dynamic DNS; captive-portal handling for travel use.

## Wireless

Radio and SSID management; security modes; guest networks; passwords and QR sharing; bands, channels, widths, and transmit power; country configuration; schedules; channel surveys; client isolation; band steering; roaming; mesh/backhaul; access point and client modes; multi-link operation when supported.

Represent supported wireless standards as extensible capability data. Show the distinction between what a radio supports, what is configured, and what a client actually negotiated. Do not assume every device supports every band, width, security mode, or newer wireless feature.

## Local networks and switching

LAN addresses and subnets; DHCP pools, leases, and options; local hostnames; IPv6 router advertisements and DHCPv6; bridges; VLANs; tagged/untagged ports; port roles and link status; isolated guest/IoT networks; static routes; multicast controls; service discovery between selected networks; link aggregation where supported.

## Firewall and access policy

Zones; inbound/outbound/forwarding rules; port forwarding; temporary rules; rule ordering and explanations; IPv4/IPv6 consistency; UPnP controls and active mappings; selective inter-network access; management access restrictions; schedule-based policies; configuration previews and validation.

## DNS and filtering

Upstream resolvers; local DNS records; split DNS; encrypted DNS where available; blocklists and allowlists; per-device or per-network filtering; exceptions; resolver diagnostics; optional query logs; retention controls; family filtering and schedules with clear limitations.

## VPN and remote access

VPN clients and servers; peer/profile management; keys and import/export; tunnel status; per-device and per-network routing; split tunneling; DNS behavior; kill switches; reconnect policies; site-to-site connections; optional overlay-network integrations. Secret handling and management exposure require explicit design.

## Traffic and performance

Current bandwidth; optional historical usage; per-device/interface totals; quotas; prioritization; SQM and queue management; latency and packet-loss tests; bufferbloat assessment; link throughput; hardware/software offload controls; resource impact explanations. Accounting, offload, and shaping may interact and need measured compatibility.

## Diagnostics and observability

System and service logs; event history; ping, route tracing, and DNS tests; interface counters; wireless diagnostics; packet capture with explicit scope; connection tracking; sanitized support bundles; external metrics export; remote logging; alert destinations; configurable retention and privacy settings.

## Administration

Admin accounts and roles; passwords and keys; session management; HTTPS certificates; SSH controls; local time and time synchronization; hostname; language and accessibility preferences; optional notifications; audit records; configuration search; consistent contextual help.

## Backup, recovery, and maintenance

Configuration export/import; encrypted backups; backup verification; selective restore where compatible; scheduled backups; configuration differences; timed confirmation and reversion for disruptive settings; service restart; reboot scheduling; factory reset; device-specific recovery guidance; optional migration assistance.

Configuration restoration, interface rollback, and firmware recovery are different operations and must be described accurately.

## Installation and updates

Compatibility inspection; authenticated router access; supported installation paths; off-device backups; versioned dashboard/software/firmware releases; authenticated release metadata; device-matched artifacts; release notes; update notifications; user-selected update policy; maintenance windows; download verification; progress and reconnection; post-update checks; migration handling; recovery guidance; offline installation.

GitHub is the intended release source. Update discovery, compatibility checks, artifact verification, and installation still need to be designed and implemented. Publishing a release alone does not make routers update.

## Optional services and extensions

USB storage; file sharing; printer sharing; cellular modems; optional monitoring integrations; local automation; a documented API; command-line access; optional modules with dependencies and resource budgets; export/import of reusable configuration profiles.

## Multiple routers and access points

Device inventory; shared configuration profiles; coordinated wireless settings; topology; staged updates; health comparison; permission boundaries; local controller options. These are candidates, not a requirement for the first implementation.

## Cross-cutting behavior

Capability discovery; shared help definitions; input validation; readable pending-change summaries; safe application of changes; authentication and authorization; resource limits; local operation without internet; accessibility; privacy; consistent errors; extensible configuration; migration and backward compatibility.

## How we will refine an idea

For each feature we choose to discuss, record its purpose, functional home, user-facing controls, contextual help, capability requirements, dependencies, permissions, failure/recovery behavior, and open questions. Assign implementation status only after we agree on its scope.
