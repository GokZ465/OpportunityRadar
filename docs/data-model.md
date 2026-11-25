# Data model

This describes the published revision-2 model. The attributes below are implemented; items in the planned section are not.

## Implemented entities

### `Opportunity`

| Attribute | Type / constraint |
|---|---|
| `Id` | Auto-generated Long Integer primary key |
| `Title` | Text(50), mandatory |
| `DateAdded` | Date Time |
| `CostType` | Text(50) |
| `SourceURL` | Text(50) |
| `Deadline` | Date |
| `Description` | Text(200) |
| `ApplicationURL` | Text(50) |
| `Reward` | Text(50) |
| `ProviderName` | Text(50) |
| `IsFeatured` | Boolean, default `False` |
| `IsActive` | Boolean, default `True` |
| `ShortDescription` | Text(100) |
| `Eligibility` | Text(50) |
| `Location` | Text(50) |
| `OpportunityType` | Text(50) |
| `Category` | Text(50) |

No source-identity or ownership attributes are present. No source identity index is present.

### `SavedOpportunity`

| Attribute | Type / constraint |
|---|---|
| `Id` | Auto-generated Long Integer primary key |
| `OpportunityId` | Mandatory foreign key to `Opportunity.Id` |
| `DateSaved` | Date Time |

### `OpportunityApplication`

| Attribute | Type / constraint |
|---|---|
| `Id` | Auto-generated Long Integer primary key |
| `OpportunityId` | Mandatory foreign key to `Opportunity.Id` |
| `Status` | Text(50) |
| `Notes` | Text(50) |
| `DateCreated` | Date Time |
| `LastUpdated` | Date Time |

### `StudentProfile`

| Attribute | Type / constraint |
|---|---|
| `Id` | Auto-generated Long Integer primary key |
| `StudentName` | Text(50) |
| `University` | Text(50) |
| `Program` | Text(50) |
| `StudyLevel` | Text(50) |
| `Interests` | Text(50) |

The profile has no user-owner field or relationship.

## Relationships

```text
Opportunity 1 ─── * SavedOpportunity
Opportunity 1 ─── * OpportunityApplication
StudentProfile   (no user relationship in the current model)
```

The two `Opportunity` foreign-key relationships are mandatory and use Protect delete behavior. Existing saved-item, application, and profile records could not be inspected in the database; their presence or contents should not be inferred from the model.

## Implemented versus planned

**Implemented:** four entities above; the `FilterOption` structure; the existing sample-data bootstrap action; a text-based demo label in seeded opportunity descriptions.

**Planned, not implemented:**

- `Opportunity.SourceName`, `ExternalID`, `StartDate`, `EndDate`, `LastSyncedAt`, `LastSeenAt`, `VerificationStatus`, and `IsDemo`
- A longer `SourceURL` suitable for canonical external URLs
- An `OpportunitySource` configuration/health entity
- A `SourceSyncLog` entity for run status, pagination, counts, and sanitized failures
- A unique composite index on `SourceName + ExternalID` for imported rows
- Ownership fields and owner-scoped indexes for saved opportunities, applications, and profiles
- Source-independent normalization, pagination, idempotent upsert, and expiry workflows

The uniqueness index must be checked against existing data before creation. Existing records must not be deleted, merged, or rewritten merely to make the index succeed. Legacy records without a known owner must not be assigned to an invented user.
