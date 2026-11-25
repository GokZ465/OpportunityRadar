# Architecture

## Existing application

OpportunityRadar is an ODC web application. Its model and runtime data are held in the OutSystems tenant; they are not files in this repository.

### User interface

The six MainFlow screens are:

1. `Dashboard`
2. `Discover`
3. `OpportunityDetail`
4. `SavedOpportunities`
5. `MyApplications`
6. `StudentProfile`

The app also contains standard Common-flow account screens. Public browsing is enabled for the MainFlow screens.

### Application logic and data flow

The current model uses server actions for operations including `SaveOpportunity`, `UnsaveOpportunity`, `AddApplication`, `UpdateApplication`, and `SaveProfile`. `BootstrapSampleData` defines the seeded sample opportunities and profile bootstrap behavior.

The application database contains four entities: `Opportunity`, `SavedOpportunity`, `OpportunityApplication`, and `StudentProfile`. See [Data model](data-model.md) for attributes and relationships.

The bootstrap timer is configured to run on publication. A prior run on revision 1 failed while inserting text values into 50-character attributes. Revision 2 increased `Description` to 200 and `ShortDescription` to 100 and added per-title seed checks. Successful insertion of the seed records after revision 2 has not been verified. No database rows were available for inspection.

## Planned integration architecture — not implemented

The proposed direction keeps ODC as the application and data hub:

1. An independent, disabled-by-default server-side workflow per authorized source.
2. Server-side normalization into the existing `Opportunity` entity.
3. Upsert identity based on `SourceName + ExternalID`, protected by a database-enforced unique composite index.
4. Per-source cursor/pagination state and run-level `SourceSyncLog` records.
5. Soft expiry only after a complete successful sync; source failures must not erase or deactivate previously imported listings.
6. Environment-specific secret references, with no credential values in entities or client-side logic.

No source timers, integrations, source registry, sync-log entity, or external API calls are part of the current application model.

## Source and export boundaries

The remote ODC MCP transport exposes model inspection and Mentor-based editing, but does not provide an OML-to-local-file download. This repository therefore does not contain a complete ODC application export, and the documentation is not a substitute for one.

No export was attempted. If a supported ODC Studio export is required, first verify the current Studio workflow and the exported artifact’s contents and licensing. Review it for embedded configuration or data before adding it to version control.
