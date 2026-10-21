# Navigation

Status: agreed working structure, recorded October 20, 2026. This defines information organization, not visual styling or completed functionality. Example tabs are proposed details to refine during feature design.

Use the [feature catalog](features.md) for behavior and the [scenario matrix](scenarios.md) for applicability. This document owns page names and placement.

## Sidebar structure

Keep nine top-level destinations and no more than two sidebar levels. The full map below includes optional destinations; installed modules and detected capabilities determine which are applicable.

```text
Overview

Devices
  All Devices
  Device Groups

Network
  Setup & Topology
  Internet Connections
  Local Networks
  Ports & Switching
  DHCP & Address Reservations
  DNS
  Routing
  Bandwidth & Prioritization

Wi-Fi
  Wireless Networks
  Radios & Channels
  Access Points & Mesh

VPN
  VPN Clients
  VPN Servers
  Site-to-Site
  Overlay Networks
  VPN Routing Policies

Security
  Firewall
  Port Forwarding
  Access Policies
  Ad Blocking & Filtering
  Guest Portal
  Automatic Port Mapping

Services
  Dynamic DNS
  File Sharing
  Printer Sharing
  Other Installed Services

Monitoring
  Traffic & Usage
  Connection Quality
  Router Health
  Events & Logs
  Diagnostic Tools

System
  Updates
  Software & Modules
  Backups & Recovery
  Administration
  Hardware & Storage
  Time & Region
  Automation
  Service Manager
  Reboot & Reset
```

The sidebar presents the main sections with relevant subsections expanded. Search and user-selected favorites provide shortcuts without changing canonical locations. Individual devices, networks, rules, and tunnels open detail pages with breadcrumbs, not deeper sidebar branches.

## Ownership boundaries

| Section | Owns | Related views |
| --- | --- | --- |
| Overview | Customizable summaries and shortcuts. | Links to the owning feature; no separate configuration copies. |
| Devices | Client identity, labels, groups, and assignments. | Reservations, filtering, VPN, and access assignments use shared editors. |
| Network | Roles, topology, connectivity, addressing, switching, routes, and bandwidth behavior. | Wi-Fi attaches to networks; Security controls access between them. |
| Wi-Fi | SSIDs, radio settings, access points, mesh backhaul, and roaming coordination. | Internet Connections references wireless uplinks without duplicating their radio configuration. |
| VPN | Outbound clients, hosted servers, site links, overlays, and VPN-specific route selection. | General and VPN routing views share route-policy objects and validation. |
| Security | Traffic permissions, isolation rules, filtering, and guest admission. | Administration separately controls access to the router's management interfaces. |
| Services | Additional functions provided by installed service modules. | Installation belongs in Software & Modules; process control belongs in Service Manager. |
| Monitoring | Measurements, history, logs, and troubleshooting. | Links to the owning settings when action is needed. |
| System | Appliance administration, software, hardware, and maintenance. | Features remain in their functional sections after installation. |

## Page boundaries

- **Setup & Topology** owns the network map and guided role changes. It identifies upstream/downstream relationships and who provides routing, DHCP, DNS, and filtering. The map may be embedded elsewhere through the same component.
- **Wireless Networks** owns SSIDs, security, and network assignments. **Radios & Channels** owns radio capabilities, channels, widths, power, and country restrictions.
- **Access Points & Mesh** covers node inventory, backhaul, and roaming as distinct views. Wired multi-AP operation does not require a wireless mesh.
- **Local Networks** owns subnets and network membership. **Ports & Switching** owns port roles, bridges, and VLAN transport. Both reference the same network objects.
- **DHCP & Address Reservations** owns address assignment. **DNS** owns resolvers and records. **Ad Blocking & Filtering** owns blocking rules and exceptions.
- **Bandwidth & Prioritization** configures traffic behavior. **Traffic & Usage** measures it.
- **VPN Routing Policies** is a VPN-focused view of shared routing policies. A rule has one identity and editor even when visible under Network and VPN. Each tunnel also has one identity across role-specific views.
- **Software & Modules** manages installation and compatibility. A service page configures that service's behavior. **Service Manager** exposes advanced runtime/startup controls and links back to the feature.

## Tabs and detail pages

Tabs divide closely related views. Advanced settings stay in labeled groups beside common controls; there is no separate miscellaneous Advanced section.

| Page or selected object | Example tabs or groups |
| --- | --- |
| Internet Connections | Connections; Failover & Load Balancing; Health Checks. |
| An internet connection | Status; Addressing; Authentication; IPv6; Advanced. DNS overrides reference the shared resolver configuration. |
| Access Points & Mesh | Access Points; Mesh & Backhaul; Roaming. |
| A VPN server | Overview; Users & Peers; Network Access; Settings; Logs. Only protocol-relevant tabs appear. |
| A VPN client | Overview; Connection Settings; Routing & DNS; Logs. |
| A device | Overview; Connection; Policy Assignments; Usage; History. |
| Administration | Accounts & Roles; Sessions; Web Access; SSH & Keys; Certificates. Backend support remains to be designed. |
| Updates | Firmware; Dashboard & Modules; Update Settings. Compatibility governs each operation. |

IPv4 and IPv6 controls belong with their relevant connection, network, or rule. Peers belong to the relevant tunnel/server, not an unrelated global list.

## Availability and module placement

| State | Presentation |
| --- | --- |
| Available | Show the feature and valid controls. |
| Not installed | Explain compatible installable functionality in Software & Modules and search. |
| Unsupported | Explain the hardware, driver, firmware, or role limitation where relevant; do not offer an unsafe action. |
| Temporarily unavailable | Keep the installed feature visible with its failure or missing dependency. |
| Unknown | Explain that detection is incomplete; do not equate uncertainty with support. |

Permissions and configured enable/disable state are separate from capability. An installed VPN with an error must remain discoverable. A change in runtime state must not silently erase a configured feature's page. Backend authorization and capability checks enforce the same restrictions as the interface.

Modules register a functional home, capabilities, permissions, labels, and help definitions. They reuse shared page and editor components. VPN modules belong under VPN, filtering modules under Security, and additional hosted services under Services. Other Installed Services is a directory of named service pages, not a mixed settings form. Installing a package alone does not imply that a custom dashboard integration exists.

## Consistent interaction

- Show defaults, inherited values, explicit overrides, and the reason an effective policy applies. Policy precedence is defined per policy type, not assumed universal.
- Reuse schedules, profiles, assignments, validation, and help components.
- Allow overview customization, favorites, table preferences, and saved views while retaining stable page locations.
- Make `(i)` help explain purpose, effects, dependencies, and defaults. Support pointer, keyboard, and touch; keep essential instructions and warnings visible.
- Preview consequential changes, identify affected networks/devices, and provide applicable confirmation and recovery behavior.
- Include names and useful synonyms in search so familiar terms such as ad blocking, bridge mode, and VPN server lead to the correct place.
