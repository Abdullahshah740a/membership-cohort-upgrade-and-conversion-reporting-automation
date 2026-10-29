# Membership Cohort Upgrade and Conversion Reporting Automation

This draft is designed to measure how many members who originally joined free later become paid members. It is a cohort-upgrade measure rather than the current paid share of all members.

> Sanitized workflow export. Deployment testing has not been performed.

## Functionalities

- **Free cohort definition:** The design identifies contacts who started free using a retained Proximity Fellow Expiration Date.
- **Upgrade definition:** The documented upgrade rule checks a paid Catalyst, Core or Circle tier, or a Membership Due Collected value.
- **Cohort conversion metric:** The intended calculation is upgraded cohort members divided by the original free cohort, multiplied by 100.
- **Shared reporting destination:** The destination is Membership Conversion in Airtable, with an upsert matched on Snapshot Key.

## Workflow

1. Start the configured weekly schedule.
2. Intended processing reads the contact population and identifies the original free cohort.
3. Intended processing counts cohort members who subsequently meet the paid-upgrade rule.
4. Calculate and map the cohort metrics before upserting the Membership Conversion snapshot.

## Tools

| Tool | Purpose |
| --- | --- |
| n8n | Weekly schedule and workflow routing. |
| JavaScript | Intended cohort calculation, not implemented in this export. |
| GoHighLevel API | Intended contact and membership field source. |
| Airtable | Configured Membership Conversion destination. |

## Repository contents

- [`workflows/workflow-v01.json`](workflows/workflow-v01.json)
- [`workflows/workflow-v02.json`](workflows/workflow-v02.json)

| Export | Nodes | Original export status | Version notes |
| --- | ---: | --- | --- |
| `workflow-v01.json` | 5 | Inactive | Alternate export corresponding to the filename ending in (1). |
| `workflow-v02.json` | 5 | Inactive | Original export without the numbered filename suffix. |

## Setup

1. Import the selected JSON file into a compatible n8n instance. All published exports are inactive.
2. Open each node and reconnect the required n8n credentials. Original credential bindings were removed.
3. Replace `EXAMPLE_*` resource identifiers, `example.com` endpoints, synthetic contacts and deployment-specific settings with your own configuration.
4. Create the required destination sheets/tables, field mappings, views and state-store schemas before writing any records.
5. Rebind Execute Workflow nodes to the corresponding workflows imported into your instance. Original workflow IDs are not portable.
6. Review prompts, scoring criteria, approval rules, spending caps and historical time windows. Keep the existing approval and no-send controls in place.
7. Use synthetic input to verify branches and destination mappings, then enable the appropriate trigger when the configuration is complete.

Credential types referenced by the original export: `airtableTokenApi`.

## Export limitations and configuration notes

- Inactive and incomplete. The computation node contains only the placeholder text cl, so the contact retrieval and conversion calculation are not implemented. Both supplied cohort exports have identical execution configurations.
- Alternate supplied versions are retained together. Review differences before selecting a version; filenames do not imply production maturity.
- Workflow export state describes the supplied file only; successful live execution has not been verified.
- Embedded client/prospect examples were replaced. Cached execution data, pinned data and credential bindings were removed.
- Resource IDs, URLs and evidence hashes were replaced for publication. Some fixtures and historical recovery scenarios require new test data and regenerated evidence.
- API credentials belong in n8n credential storage or the configured secret store. Do not commit live keys, contact lists or execution receipts.

## Validation

The preparation checks parse the JSON, preserve node counts and check connection targets. Code-node syntax is checked separately without executing the workflow. These checks do not verify provider access, business results or production readiness.
