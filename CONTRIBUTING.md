# Project standards

These standards record the owner's requirements. Apply them to documentation, implementation, reviews, and future contributions.

## Organization

Give each file and module a clear responsibility and a predictable home. Group related functionality together. Keep shared functionality in one maintained location. Do not create speculative folders, duplicate documents, abandoned drafts, or miscellaneous dumping grounds.

Create implementation directories only when there is implementation to put in them. Keep generated files and temporary work out of source directories. Remove obsolete files and references as part of the change that replaces them.

Use descriptive names. Documentation filenames use lowercase words separated by hyphens; preserve conventional names such as README.md and CONTRIBUTING.md. Choose language-specific naming conventions before introducing code and apply them consistently.

## Modularity and reuse

Prefer small, cohesive modules with explicit interfaces. Reuse shared validation, controls, help indicators, configuration handling, and capability checks. Avoid duplicated logic and cosmetic variations of the same component.

Keep configurable values and device-specific behavior out of shared feature logic. Use configuration, feature definitions, and isolated device adapters where appropriate. Fixed protocol values and genuine invariants may be constants with clear names. Avoid unnecessary abstractions: reuse should make code easier to understand and maintain.

## Hardware capabilities

A product name alone must not determine the interface. Distinguish hardware capability, driver support, installed service availability, regulatory restrictions, configured state, and current operating state.

Features should declare their requirements and use a shared capability mechanism. Distinguish available, not installed, unsupported, temporarily unavailable, and unknown capabilities. Keep permissions and configured enable/disable state separate. Unsupported operations must also be rejected by the backend; hiding a control is insufficient.

Allow new capabilities and standards to be added without duplicating entire pages. Detection cannot make unsupported hardware or firmware compatible. Exact firmware images still require device-specific compatibility validation.

## Interface consistency

Use the owner's modular templates and styled elements when design work begins. Keep feature behavior independent of presentation wherever practical. Defer layout and visual decisions until those resources are available.

Give every setting a clear functional home. Reuse shared components for repeated controls and contextual information indicators. Help text should explain purpose, effect, and relevant dependencies in plain English. Information indicators must work with keyboard focus and touch, as well as pointer input. Essential instructions and errors must remain visible without opening a tooltip.

## Code and writing

Use clear, professional English, consistent terminology, correct grammar, and punctuation. Prefer straightforward names over clever abbreviations. Comments should explain intent, constraints, or surprising behavior rather than repeat the code.

Select formatting and linting tools when languages are chosen, then enforce them consistently. Keep error messages actionable and distinguish user-facing explanations from technical diagnostics. Centralize repeated labels and help text when implementation begins.

## Changes and quality

Keep changes focused. Update the owning documentation instead of adding overlapping explanations. Check applicable behavior, compatibility, accessibility, and error paths. Add meaningful tests for reusable logic and consequential operations.

Keep credentials, router backups, private keys, and personal network information outside the repository. Versioned releases must distinguish published software from ongoing development. Do not claim hardware support or recovery guarantees without evidence.

## Maintaining the plan

Keep one owning document for each concern: `docs/navigation.md` for page names and placement, `docs/features.md` for feature behavior, and `docs/scenarios.md` for applicability and future acceptance checks. The README is the entry point; hardware observations stay in `docs/hardware.md`.

When a feature changes, update its owning entry and any affected navigation or scenarios in the same change. Use stable feature and scenario IDs when linking future issues or specifications. Keep proposed details and open questions distinct from agreed direction, implementation, and test evidence. Do not turn a planning entry into a support claim.

Prefer extending these documents over creating overlapping drafts. Add a focused specification only when a feature needs enough detail to justify its own file, and link it from the catalog. Choose implementation directories, language-specific conventions, and automation when the corresponding work begins.
