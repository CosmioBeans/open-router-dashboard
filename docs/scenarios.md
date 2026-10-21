# Scenario matrix

## Status and scope

Recorded October 20, 2026.

This document records the agreed need to account for different network arrangements, including upstream routers, access points, mesh nodes, extenders, bridges, and networks without internet access. The detailed behaviors and acceptance checks below are **proposed requirements for review**, not completed or tested functionality. Listing a scenario does not establish support on a particular router.

The scenario matrix complements the [navigation plan](navigation.md) and [feature catalog](features.md). It does not add sidebar sections. The relevant configuration homes are:

- **Network → Setup & Topology:** the router's role, uplinks, topology, and guided setup.
- **Wi-Fi → Access Points & Mesh:** access points, mesh backhaul, and roaming.
- **Security → Ad Blocking & Filtering:** filtering policies, exceptions, and their coverage.

Detailed settings retain the homes defined in the navigation plan. A setup flow uses those shared settings and editors; it does not maintain a second configuration.

## Modeling rules

- Treat routing, address translation, bridging, wireless access, and wireless uplinks as capabilities that can be combined. A preset describes a useful combination; it is not an exclusive identity for the whole router.
- Treat upstream and downstream as relationships. A downstream router can also supply Wi-Fi, host a VPN, and manage several local networks.
- Record which component provides DHCP, DNS, routing, and policy enforcement for each network. Do not assume this router owns every service.
- Distinguish managed equipment from equipment that is only discovered or observed. Discovery does not grant configuration access.
- Distinguish current observations, inferred relationships, configured intent, and unknown information.
- Identify the exact link or network being bridged. Do not present one universal “Bridge Mode” switch for unrelated arrangements.

Scenario IDs are stable references. Use the same ID across the following tables, discussions, and future tests, even if a scenario's display name changes.

## Roles and service ownership

| ID | Scenario | Network arrangement | DHCP, DNS, and routing responsibility |
| --- | --- | --- | --- |
| S01 | Primary gateway | This router connects local networks to an internet uplink. | This router usually supplies local DHCP and DNS and owns routing and firewall policies. Support explicit external DHCP or DNS services. |
| S02 | Downstream router | This router sits behind another router and serves a separate subnet. | This router may supply downstream DHCP and DNS. Both routers participate in routing. NAT is an explicit choice; operation without downstream NAT requires appropriate upstream routes. |
| S03 | Wired access point | Ethernet and wireless access extend an existing local network. | The upstream network normally owns DHCP, DNS, and routing. This device needs a reachable management address and must not accidentally introduce a second DHCP server. |
| S04 | Routed wireless uplink or travel router | An existing Wi-Fi network provides the uplink to a separate local network. | This router can own local DHCP, DNS, and routing. The upstream network owns its own services. Captive-portal access and changes of upstream network require separate handling. |
| S05 | Wireless extender on the existing network | Wireless backhaul extends an existing local network. | Upstream services normally remain authoritative. The selected bridge or relay method must declare its actual behavior and limitations. |
| S06 | Wireless client adapter | A wireless uplink connects wired equipment; a local Wi-Fi access point is optional. | Ownership depends on whether the supported arrangement is routed or bridged. The setup must state which arrangement will be used. |
| S07 | Mesh node | A node participates in wireless backhaul and may also provide client Wi-Fi or gateway functions. | Assign service ownership per network. Joining a mesh must not automatically enable DHCP, DNS, or internet gateway functions on every node. |
| S08 | Multiple access points with wired backhaul | Several access points serve a network over Ethernet. | The designated gateway or external servers provide network services. Access-point settings and roaming can be coordinated without requiring wireless mesh. |
| S09 | Multiple internet connections | Two or more uplinks provide failover, load balancing, or policy-selected paths. | This router manages uplink and path selection. DHCP and DNS ownership remains explicitly assigned for each local network. DNS, VPN, and IPv6 behavior must be defined for each uplink and failure condition. |
| S10 | Segmented networks | Guest, work, IoT, or other networks share infrastructure with explicit isolation. | Declare DHCP, DNS, routing, and access policies per network. VLAN membership and transport must remain consistent across participating ports and backhaul links. |
| S11 | VPN gateway or network-to-network connection | Selected devices or networks use a VPN, or remote networks connect through one. | Existing network roles remain in place. Explicit policies determine DNS ownership, routed prefixes, VPN access, and behavior when a tunnel fails. |
| S12 | Local network without internet access | Devices use local networking and services with no usable internet connection. | Local services may run on this router or another local system. Local management and diagnostics remain available independently of internet status. |
| S13 | Transparent Ethernet bridge | Selected wired interfaces bridge an existing network without creating a routed boundary. | Upstream services normally remain authoritative. Management has an explicit address and access path. Any inspection or enforcement needs a supported bridge-specific implementation. |
| S14 | Third-party or unmanaged network equipment | Existing routers, extenders, switches, or proprietary mesh systems remain outside this project's management. | The external equipment retains its responsibilities. Represent known service ownership and topology without assuming enrollment, control, or complete visibility. |

OpenWrt distinguishes 802.11s mesh backhaul from client roaming, and mesh availability depends on the wireless driver. This is why S07 and S08 remain separate scenarios. [OpenWrt mesh documentation](https://openwrt.org/docs/guide-user/network/wifi/mesh/802-11s)

Wireless bridging also needs an explicit implementation choice. OpenWrt documents `relayd` as an IPv4 pseudo-bridge; it must not be presented as interchangeable with a fully transparent bridge. [OpenWrt relayd documentation](https://openwrt.org/docs/guide-user/network/wifi/wifiextenders/relay_configuration)

## Feature references

The catalog defines stable feature IDs. Setup and topology use F04; network service ownership uses F05–F11; wireless roles use F13–F15; VPN behavior uses F16–F19; enforcement and filtering use F20–F25; measurement uses F29–F33; and maintenance/recovery use F34–F40. Apply the shared product behavior to every scenario.

## Policy and measurement applicability

The product must show the scope in which a feature works. A feature being installed does not mean every device's traffic or DNS queries pass through it. Measurements must identify their observation point and avoid counting the same traffic repeatedly across interfaces or managed nodes.

| Scenario IDs | Ad blocking and filtering | VPN behavior | Traffic accounting |
| --- | --- | --- | --- |
| S01, S02 | Apply policies to DNS queries or traffic handled by the configured enforcement component. Show exceptions and paths outside that coverage. | Support device and network policies, with explicit routing and failure behavior. | Report locally observed traffic. Do not claim visibility into unrelated upstream networks. |
| S03, S08 | Offer filtering only when clients actually use the configured resolver or an applicable enforcement service. AP mode alone does not establish coverage. | Distinguish the access point's own VPN connection from a VPN path for client traffic. | Show measurements available at each AP and a separate aggregated view when managed-node reporting is available. |
| S04 | Explain whether filtering is local, upstream, or supplied through a VPN. Captive-portal access needs a visible, scoped exception mechanism if required. | Show whether local devices currently use the VPN and what happens before the uplink or tunnel is ready. | Separate local traffic from wireless-uplink usage where the available measurements allow it. |
| S05, S06 | Derive coverage from the selected routed, bridged, or relay arrangement. Do not inherit gateway assumptions. | Enable client-traffic routing only when the actual arrangement supports the required path. | Describe which devices and interfaces are observable. Mark unavailable breakdowns rather than displaying zero. |
| S07 | Assign filtering responsibility to the relevant gateway or resolver instead of silently duplicating it on every node. | Identify which node owns each tunnel and which networks use it. | Distinguish client traffic, backhaul traffic, and transit traffic. Avoid inflating network totals through repeated observations. |
| S09 | Define resolver selection and filtering coverage during failover. | Define which uplinks a tunnel may use and whether affected traffic stops or falls back when the tunnel fails. | Separate per-uplink usage from network totals and record path-change events. |
| S10 | Support different policies per network and clearly explain inherited settings and exceptions. | Bind policies to the intended networks, devices, and destinations. | Provide network-level views where reliable data is available, without exposing restricted details to unauthorized administrators. |
| S11 | Show whether DNS resolution occurs locally, through the tunnel, or elsewhere. | Distinguish VPN client, server, and network-to-network roles and their access policies. | Separate tunnel transfer counters from inner device traffic; do not simply add them together. |
| S12 | Local filtering and local DNS can continue where their dependencies remain available. Show when external list updates or upstream resolution are unavailable. | Show unavailable remote connections without treating the entire local network as failed. | Continue local measurements within configured resource and storage limits. |
| S13 | Do not promise routed firewall or DNS-filtering behavior merely because traffic crosses a bridge. Declare supported enforcement explicitly. | Do not imply that creating a tunnel automatically redirects bridged client traffic into it. | Show bridge/interface data only to the extent supported by the platform and measurement method. |
| S14 | Describe only coverage established through a managed enforcement point. | Do not assume control of tunnels or routing policies on unmanaged equipment. | Label inferred topology and partial measurements. Hidden downstream devices must remain unknown rather than invented. |

## Dependencies, management, and recovery

| Scenario IDs | Dependencies or checks before applying changes | Management and recovery requirements |
| --- | --- | --- |
| S01, S02 | Validate addressing, routing, upstream reachability, and service ownership. Detect subnet overlap. Report evidence of possible upstream NAT without treating a private WAN address as proof of double NAT. | Show the resulting management address and access path. Use timed confirmation and rollback where the platform can support them reliably. |
| S03, S08 | Verify wired connectivity, management addressing, DHCP ownership, and participating access-point capabilities. | Preserve local access if coordination with other APs is lost. Stage configuration changes across managed nodes. |
| S04 | Check supported simultaneous wireless roles and the uplink's addressing and access requirements. | Provide a local recovery path when an upstream SSID changes, disappears, or requires portal access. |
| S05, S06 | Verify the actual wireless bridge, relay, or routed method, peer requirements, and IPv4/IPv6 behavior. | Explain where management remains reachable. Provide a recovery address or other supported procedure if the uplink fails. |
| S07 | Verify mesh/driver support, peer authentication, network membership, and any VLAN transport assumptions. | Detect disconnected nodes and stale observations. A controller outage must not be confused with a node's loss of forwarding capability. |
| S09 | Validate health-check targets, path priorities, metered-link policies, and per-uplink IPv6 and DNS settings. | Protect the management path from route changes. Record failover cause and current path rather than reporting only a generic disconnection. |
| S10 | Validate VLAN tagging, port membership, policy assignment, and management-network reachability across all affected managed links. | Preview affected devices and ports. Prevent or clearly identify a configuration that removes the administrator's access path. |
| S11 | Check tunnel capabilities, route overlap, access policies, DNS selection, and declared failure behavior. | Keep administration reachable through an explicitly selected path. Explain configuration that intentionally permits management only over a VPN. |
| S12 | Identify services that need external DNS, time synchronization, downloads, or authentication. | Keep local administration available. Mark unavailable external dependencies without continuously restarting healthy local services. |
| S13 | Verify bridge support, port membership, loop prevention where applicable, and a separate management path. | Offer a supported recovery procedure for incorrect port membership or loss of management connectivity. |
| S14 | Require explicit enrollment before using any management capability. Discover capabilities and permissions instead of assuming them. | Link to available external management information when known. Never describe a requested change as applied to equipment the project cannot control. |

OpenWrt's extender documentation highlights that relay configurations have particular management-address and reachability requirements. Recovery behavior therefore belongs in setup rather than being left to troubleshooting after a disconnection. [OpenWrt repeater documentation](https://openwrt.org/docs/guide-user/network/wifi/wifiextenders/relay_configuration)

## Interactions to validate

Scenarios are composable. Future implementation must evaluate the combination, not only the individual feature switches.

- **IPv6:** verify addressing, prefix delegation, router advertisements, routing, DNS, firewall policy, and VPN coverage separately from IPv4. Do not treat IPv4 success as evidence of IPv6 correctness.
- **VLANs over backhaul:** verify that the selected wired or wireless transport carries the intended networks end to end. Unsupported combinations need an explanation before application.
- **Upstream NAT and subnet collisions:** distinguish observations from suspected causes. An overlapping subnet is a concrete configuration conflict; a private uplink address alone does not prove a complete NAT topology.
- **Management access:** evaluate changes to addresses, VLAN membership, routes, VPN policies, and firewall rules together. Show the next access method before a disruptive change.
- **Multiple service providers:** identify intended DHCP, DNS, and gateway owners. Warn about conflicting observed providers without assuming that every external service is unauthorized.
- **Roaming and backhaul:** report client association and backhaul health separately. A healthy backhaul does not establish that a client transition succeeded.
- **Unmanaged nodes:** retain unknown relationships and limited control in maps, policy previews, and troubleshooting. Do not silently convert inferred equipment into managed nodes.
- **Offline operation:** local management, saved help, and existing configuration remain useful when internet access, package downloads, or release checks fail.
- **Resource limits:** declare telemetry sampling, retention, storage location, and supported detail. Optional history must not silently consume all router storage.

## Proposed acceptance checks

These are future checks to guide implementation. None are claims that the project has passed them.

1. **Ownership and navigation — all scenarios:** selecting a setup preset shows the resulting service owners and configuration changes. Opening the same setting from setup or its canonical page edits the same object.
2. **Downstream routing — S02:** test both NAT and explicitly routed operation, an overlapping subnet, a private upstream address, and an unreachable upstream gateway. The interface distinguishes observed facts from suspected double NAT.
3. **Access-point management — S03, S08:** switch a managed test device to AP operation. Confirm that the intended upstream server supplies client addresses and that the displayed management path works. Test recovery after losing the uplink.
4. **Wireless extension — S04–S07:** exercise supported routed and bridged arrangements separately. Reject unsupported combinations before application, and describe their effect on DHCP, DNS, IPv6, and management access.
5. **Multi-node visibility — S07, S08, S14:** combine managed and unmanaged equipment. Confirm that the map labels unknown or inferred links and offers configuration actions only for equipment with established management access.
6. **Failover and VPN policy — S09, S11:** interrupt an uplink and a tunnel independently. Confirm that traffic, DNS, and status follow the declared fallback or blocking policy and that events identify the affected path.
7. **Segmentation — S07, S08, S10:** verify permitted and prohibited communication across guest and management networks over each supported backhaul. Include an intentional VLAN mismatch and verify that the diagnostic explanation is specific.
8. **Filtering coverage — all applicable scenarios:** compare clients using the configured resolver with clients outside that resolver's scope. Confirm that the dashboard reports measured filtering coverage rather than claiming universal protection.
9. **Offline behavior — S12:** remove internet access while retaining the local network. Confirm local login, configuration, local diagnostics, and clear dependency status without an internet-required setup loop.
10. **Measurement integrity — all applicable scenarios:** compare known traffic with interface, tunnel, and aggregated counters. Verify scope labels, missing-data states, reset handling, timestamps, and avoidance of duplicate totals.
11. **Management recovery — all disruptive changes:** simulate a change that would remove the active administration path. Verify the supported confirmation or recovery procedure and report failures without claiming a rollback succeeded.
12. **IPv6 parity — S01, S02, S09–S11:** verify policy, addressing, DNS, and connectivity for both protocol families. Show partial success accurately when only one family is working.
