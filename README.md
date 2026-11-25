# OpportunityRadar

OpportunityRadar is an OutSystems Developer Cloud (ODC) web application concept for helping University of Waterloo students discover opportunities such as events, scholarships, and hackathons.

> **Repository scope:** This repository contains project documentation only. The ODC application model (OML), generated application source, and database contents have not been exported. Do not treat these documents as a deployable application.

## Current status

- The existing ODC application is published at revision 2 in its Development environment.
- Its current model contains six MainFlow screens and four application entities.
- The app is currently a demo/sample-data application. Multi-source ingestion and source-sync infrastructure are planned, not implemented.
- Twelve sample opportunities are defined by the bootstrap action. Successful insertion of all twelve records into the Development database has not been verified.
- No external source API is connected.
- Phase 1 integration-foundation changes are not present in the published model.

Tenant URLs, asset identifiers, environment configuration, credentials, and personal information are intentionally omitted.

## Existing features

The current model includes:

- Dashboard summaries and featured/recent opportunities
- Opportunity discovery with search and filters
- Opportunity detail pages and application links
- Saved opportunities
- Application tracking
- A student profile
- Demo notices warning visitors not to enter sensitive information

These are model-level features; this documentation does not independently verify every runtime behavior.

## Technology

- OutSystems Developer Cloud (ODC)
- ODC web application model and server-side entities/actions
- ODC database and a sample-data bootstrap timer

There are no source integrations or API credentials in this repository.

## Documentation

- [Architecture](docs/architecture.md)
- [Data model](docs/data-model.md)
- [Roadmap](docs/roadmap.md)
- [Security](docs/security.md)

## Application model export

The available remote ODC MCP tools do not expose a download of the server-side OML model. No export was attempted, and no application source file is present here. See [Architecture](docs/architecture.md#source-and-export-boundaries) for the limitation and safe next step.
