# Roadmap

## Current state

The published revision-2 application is a demo/sample-data app. The integration foundation, source-specific APIs, and synchronization workflows are not implemented. API keys, authorized calendars, provider agreements, and source permissions have not been supplied or verified.

## Phases

### Phase 0 — Access and source verification

- Confirm an official API/feed and its terms for every candidate source.
- Obtain credentials and owner authorization through the provider’s supported process.
- Confirm each API actually provides the needed Waterloo-area events, scholarships, funding, or hackathons.
- Establish refresh frequency, retention, attribution, and permissible display fields.
- Do not scrape sources without authorization.

### Phase 1 — Integration foundation

- Add source identity, event dates, sync timestamps, verification status, and `IsDemo` to `Opportunity`.
- Add `OpportunitySource` and `SourceSyncLog`.
- Add safe indexes, including a unique source identity index.
- Build source-independent normalization, pagination, duplicate-safe upsert, and failure logging.
- Keep each source workflow disabled until its access is approved and configured.
- Keep public browsing while requiring authenticated, owner-scoped server-side writes for personal activity.

### Phase 2 — Authorized pilot sources

- Evaluate the University of Waterloo Open Data API only after confirming that its current API catalogue includes the required opportunity/event datasets.
- Integrate Luma only for calendars whose owners authorize access and provide calendar-scoped credentials.
- Add other sources only when an official feed/API and the necessary permissions are confirmed.

### Phase 3 — Additional provider integrations

Potential sources remain conditional:

| Source | Current feasibility note |
|---|---|
| Waterloo Open Data | API v3 and API-key process are documented; relevant opportunity/event dataset coverage still needs confirmation. [Getting started](https://uwaterloo.atlassian.net/wiki/spaces/UWAPI/pages/34025641600/Getting+Started+-+OpenAPI) · [API spec](https://openapi.data.uwaterloo.ca/swagger/v1/swagger.json) |
| Luma | Requires Luma Plus and an authorized calendar API key. Calendar event-list access is scoped; view-access events can have reduced details. [API guide](https://docs.luma.com/reference/getting-started-with-your-api) · [List events](https://docs.luma.com/reference/get_v1-calendars-events-list) |
| Eventbrite | The public Search Events endpoint was shut down in 2019. General public discovery is not available through that endpoint; organizer-authorized access would be a different, narrower scope. [API reference](https://www.eventbrite.com/platform/new/api#/reference/event-search/list-events) |
| MLH | Official event listings exist, but no approved public API/feed was verified. [Event directory](https://mlh.io/seasons/2026/events) |
| Devpost | No approved public API/feed was verified in this review. |
| Mitacs | Official program listings exist, but no API/feed was verified. [Programs](https://www.mitacs.ca/programs-resources/programs/) |
| Wat2Do | An authorized API/feed and access terms remain unverified. |

No scraping is planned for MLH, Devpost, Mitacs, Wat2Do, or any other source without the owner’s authorization.

### Phase 4 — Safety and rollout

- Test retries, 429 handling, partial pagination, duplicate upserts, and source outages.
- Preserve existing opportunities and user activity; expire records only after a complete successful source scan and an agreed grace period.
- Verify anonymous users can browse but cannot access or mutate another user’s profile, saved items, or applications.
- Review logs for credential or personal-data leakage.
- Enable one approved source at a time; validate results before enabling another.

## Complexity

The overall effort is large and access-dependent. The shared foundation is a significant model/security change; each approved API adapter is a separate integration. Sources without a documented authorized feed cannot be estimated until providers confirm access.
