# MLOps_NSH_Project

The Agentic Reporting Platform (ARP): the final project for DADS 7305 (Machine Learning Operations), built for Nonstop Health (NSH).

> Ask NSH's data a question in English; get a validated, interactive, access-controlled report.

> **Status:** this repository currently holds the planned structure only. Code is added as the project progresses. Items marked **Decision pending** are not decided yet; items marked **To be filled in** can only be written once the code exists.

## Project information

ARP is a Python application driven by a large language model (LLM). It replaces the current process of building and embedding Tableau and QuickSight dashboards. A user asks for a report in plain English, the system generates a validated, read-only MongoDB query against a governed data layer, processes the result in Python, checks the numbers, and then displays interactive widgets.

**In scope**

- A web reporting app where users ask questions in plain English or choose a saved report and filters.
- An agentic pipeline that interprets the request, plans, generates a validated query, processes the result, displays widgets and validates the output.
- A semantic layer (contract registry) describing collections, columns, field definitions, allowed values, join keys, money units, business formulas and which fields hold PHI.
- Saved reports that can be parameterized, scheduled and shared.
- Migration of the current dashboards and the still-active Reports Engine exports.
- Scheduled delivery by email, PDF and Excel, replacing the weekly KPI email.
- Embedding reports back into the NSH portals.

**Out of scope (version 1)**

- Rebuilding NSH's operational systems: WEX integration, Shield and the billing engine.
- Predictive machine learning and risk modeling as a headline feature.
- Replacing the NetSuite and QuickBooks accounting systems.
- Carrier EDI 834 enrollment files. **Decision pending:** whether the carrier-format Excel feeds in the Reports Engine move to the new platform.

## Repository structure

| Folder | Contents |
|---|---|
| `api/` | API gateway: sign-in check and server-side access control (FastAPI) |
| `agent/` | Orchestrator and LLM steps: understand, plan, generate the query, choose charts, narrate |
| `semantic_layer/` | Versioned YAML/JSON configuration, read by the model and the validator |
| `validation/` | Checks before a query runs, and pandas processing and result checks after |
| `ui/` | Widget UI: Streamlit for the internal MVP |
| `jobs/` | Scheduler and delivery: scheduled and background reports, delivered by email, PDF or Excel |
| `tests/` | Golden-output tests and unsafe-prompt tests, run with pytest |
| `data/synthetic/` | The synthetic-data generator, built from NSH's data contract. No real data |
| `infra/` | Terraform, which defines the infrastructure as code |
| `.github/workflows/` | GitHub Actions pipeline |
| `docs/` | Runbooks and documentation handed over to NSH |
| `README.md` | This file |

Each folder has its own short README. The folders above map to the components of the platform.

**Decision pending:** final folder names.

## Installation

- Prerequisites: Python 3.11+, Docker, and FastAPI with Pydantic, pymongo and pandas.
- **To be filled in:** the installation commands, once the local development setup is decided.

## Synthetic data

Development and test use synthetic, non-PHI data generated from NSH's data contract. No real data is committed. The synthetic database must run MongoDB 5.0 or newer.

**To be filled in:** how to generate or restore the synthetic dataset and check that it loaded.

## Running

The internal MVP uses Streamlit.

**To be filled in:** the start command, and one worked example: a question and the report it returns, once the first report works.

## Tests

Tests run with pytest and include the golden-output tests and the unsafe-prompt tests.

**To be filled in:** the test commands.

## Configuration and secrets

No long-lived keys in code or configuration. In AWS, each service has one task role and secrets are kept in AWS Secrets Manager.

## Release

A change goes through a pull request reviewed by NSH's data and platform leads, GitHub Actions with pytest, a Docker image build, development and test on synthetic data, and a security review before NSH production. Production is operated by NSH.

**Decision pending:** the deployment and rollback approach.

## Operations

The runbooks and documentation are handed over to NSH in Phase 5 and live in `docs/`.

## Contributing

- Every change is a pull request reviewed by NSH's data and platform leads, with a golden-output test for every report change.
- Semantic-layer changes are versioned and reviewed like code.
- A golden-output or unsafe-prompt test that fails stops the change from being merged or released.
- A weekly demo runs against the synthetic dataset.
- A security review must pass before any connection to a production replica.
- We build and test on synthetic, non-PHI data.

## Team

**To be filled in:** team members.
