# mds-profile

The **Mobility Data Space dataspace profile**: the data space specifications between the participants of the MDS, the MDS Authority and the MDS Trusted Issuers for the dataspace to work.

| Role | Responsibility |
|---|---|
| MDS Trusted Issuers | issues MDS credentials |
| MDS Authority | governs: decides membership and groups, and defines the usage policies and the data offers vocabulary that participants follow |
| Participant | provides and consumes data within the MDS, following the usage policies and data offers vocabulary |

## Versions

| Version | Specification | Status |
|---|---|---|
| `2026/1` | [`2026/1/mds-2026-1.md`](2026/1/mds-2026-1.md) | DRAFT |

## Layout

The repository mirrors the URI space of the profile, so published artefacts sit at the path their identifiers resolve to:

```
2026/1/mds-2026-1.md                                     the profile specification
2026/1/policy/mds-odrl-profile-2026-1.md                 ODRL profile specification
2026/1/policy/context.jsonld                             policy JSON-LD context
2026/1/credentials/context.jsonld                        credentials JSON-LD context
2026/1/credentials/mds-credentials-2026-1.md             credential specification
2026/1/credentials/MembershipCredential.schema.json      MembershipCredential JSON Schema
2026/1/credentials/GroupMembershipCredential.schema.json GroupMembershipCredential JSON Schema
2026/1/vocabulary/mds-vocabulary-2026-1.md               data offers vocabulary specification
2026/1/vocabulary/context.jsonld                         data offers vocabulary JSON-LD context
examples/                                                non-normative examples
```

A future profile version is added as a sibling directory (`2027/1/`, …).

## Identifiers

Everything is addressed through the [w3id.org](https://w3id.org) namespace `mobility-dataspace`, which redirects to MDS specifications. Consumers **MUST** use the `w3id.org` identifiers, never the `github.io` targets — the latter are an implementation detail and may move.

| Identifier | Resolves to |
|---|---|
| `https://w3id.org/mobility-dataspace/2026/1/` | the profile specification |
| `https://w3id.org/mobility-dataspace/2026/1/policy/` | the ODRL profile namespace; resolves to the ODRL profile specification |
| `https://w3id.org/mobility-dataspace/2026/1/policy/context.jsonld` | the policy JSON-LD context |
| `https://w3id.org/mobility-dataspace/2026/1/policy/Membership` | the `Membership` left operand; resolves to its section of the ODRL profile specification |
| `https://w3id.org/mobility-dataspace/2026/1/policy/ParticipantId` | the `ParticipantId` left operand; resolves to its section of the ODRL profile specification |
| `https://w3id.org/mobility-dataspace/2026/1/policy/Group` | the `Group` left operand; resolves to its section of the ODRL profile specification |
| `https://w3id.org/mobility-dataspace/2026/1/policy/EvaluationTime` | the `EvaluationTime` left operand; resolves to its section of the ODRL profile specification |
| `https://w3id.org/mobility-dataspace/2026/1/policy/ManualApproval` | the `ManualApproval` left operand; resolves to its section of the ODRL profile specification |
| `https://w3id.org/mobility-dataspace/2026/1/credentials/` | the credentials vocabulary namespace; resolves to the credential specification |
| `https://w3id.org/mobility-dataspace/2026/1/credentials/context.jsonld` | the credentials JSON-LD context |
| `https://w3id.org/mobility-dataspace/2026/1/credentials/MembershipCredential` | the MembershipCredential type; resolves to its section of the credential specification |
| `https://w3id.org/mobility-dataspace/2026/1/credentials/GroupMembershipCredential` | the GroupMembershipCredential type; resolves to its section of the credential specification |
| `https://w3id.org/mobility-dataspace/2026/1/credentials/groups` | the `groups` claim; resolves to its definition in the credential specification |
| `https://w3id.org/mobility-dataspace/2026/1/credentials/MembershipCredential.schema.json` | the MembershipCredential JSON Schema |
| `https://w3id.org/mobility-dataspace/2026/1/credentials/GroupMembershipCredential.schema.json` | the GroupMembershipCredential JSON Schema |
| `https://w3id.org/mobility-dataspace/2026/1/vocabulary/` | the data offers vocabulary namespace; resolves to the data offers vocabulary specification |
| `https://w3id.org/mobility-dataspace/2026/1/vocabulary/context.jsonld` | the data offers vocabulary JSON-LD context |
