# Security

## Current limitations

- All six MainFlow screens are configured for anonymous access. Public browsing is intentional, but the current model does not make personal activity private.
- `SavedOpportunity`, `OpportunityApplication`, and `StudentProfile` have no user-owner field.
- Server actions for saving/unsaving opportunities, adding/updating applications, and saving profiles do not currently enforce per-user ownership.
- Visitors can therefore write shared records, and data may be visible to other visitors. A demo notice warns users not to enter personal or sensitive information.
- Prior validation reported anonymous-write security warnings. The available reports disagreed on the overall warning count (25 versus 26); rerun validation before relying on a count.
- No external API credentials or integrations are implemented in the published revision-2 model.

Do not use the current app for confidential student information or assume anonymous records are private.

## Planned controls

- Keep opportunity browsing anonymous, but require an authenticated identity for profile, saved-opportunity, and application writes.
- Add ownership identifiers to personal records and enforce ownership in server actions and data queries; hiding a UI control is not authorization.
- Preserve existing ownerless rows. Do not assign them to a guessed user; decide on a safe migration or archive policy before exposing them as personal records.
- Keep source synchronization server-side and inaccessible to anonymous callers. Leave timers disabled until a source is authorized and configured.
- Store provider secrets only in environment-specific secure configuration. Store, at most, a non-secret reference/alias in source configuration records; never put key values in the app database, client code, documentation, or Git.
- Sanitize sync logs and avoid recording authorization headers, tokens, private personal data, or full request payloads.

## Repository safeguards

The local workspace contains MCP/IDE configuration and workspace-specific instructions, not application source. Those files are excluded from version control. No tenant URL, asset identifier, credential, API key, personal data, or environment secret is included in this repository.
