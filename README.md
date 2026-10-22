# Open Router Dashboard

A modular router administration and firmware project built around OpenWrt. The aim is extensive control, useful data, and a clear interface that adapts to the router's capabilities and its role in the network.

**Status: planning.** The navigation and product direction below are agreed working foundations. No dashboard, installer, firmware, or updater has been implemented, and no hardware has been tested with project software. Release scope and implementation choices remain open.

The working name is `open-router-dashboard`. Development and future versioned releases use one [public GitHub repository](https://github.com/CosmioBeans/open-router-dashboard).

## Start here

| Document | Responsibility |
| --- | --- |
| [Navigation](docs/navigation.md) | The agreed page structure, functional ownership, and navigation behavior. |
| [Feature catalog](docs/features.md) | Planned capabilities, shared behavior, constraints, and ideas still under consideration. |
| [Scenario matrix](docs/scenarios.md) | How roles, topology, dependencies, and recovery affect feature applicability. |
| [Project standards](CONTRIBUTING.md) | Organization, reuse, naming, writing, and contribution practices. |
| [Hardware research](docs/hardware.md) | Existing device observations; hardware investigation is currently deferred. |

## Product principles

- Support compatible routers broadly; the initial research devices do not define the product's limits.
- Determine availability from hardware, drivers, firmware, installed modules, permissions, and network role.
- Keep common tasks approachable while placing advanced controls beside the feature they affect.
- Give settings one authoritative home and reuse the same editors, validation, and configuration elsewhere.
- Reuse the owner's modular HTML templates and styled components when interface work begins. Visual styling is deferred.
- Make contextual information accessible through shared `(i)` controls; keep essential instructions visible.
- Support customizable summaries, favorites, device groups, and reusable policies without making navigation unpredictable.
- Explain the scope and limits of measurements, discovered topology, filtering, and recovery.
- Keep local administration usable without internet access.
- Distribute verified, compatible releases through GitHub; release publication and router installation are separate operations.

## How the plan evolves

The documents distinguish agreed direction, proposed detail, and open decisions. Planned scope is not a commitment to ship every feature in the first release. New ideas belong in the relevant existing document; add files only when a new responsibility warrants one.

Before implementing a feature, define its capabilities, scenario coverage, permissions, data ownership, failure behavior, and acceptance checks. Frameworks, backend choices, licensing, installer platforms, update policy, and release sequencing still need decisions.
