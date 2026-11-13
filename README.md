# mds-profile

The **Mobility Data Space dataspace profile**: the data space specifications between the participants of the MDS, the MDS Authority and the MDS Trusted Issuers for the dataspace to work.

| Role | Responsibility | Specified in |
|---|---|---|
| MDS Authority | governs the dataspace: decides membership and groups, and defines the usage policies and the data offers vocabulary that participants follow | the [credentials lifecycle](2026/1/credentials/mds-credentials-2026-1.md#credentials-lifecycle), the [ODRL profile](2026/1/policy/mds-odrl-profile-2026-1.md), the [data offers vocabulary](2026/1/vocabulary/mds-vocabulary-2026-1.md) |
| MDS Trusted Issuers | issue the MDS credentials | [Issued Credentials](2026/1/credentials/mds-credentials-2026-1.md#issued-credentials), the [credential definitions](2026/1/credentials/mds-credentials-2026-1.md#mds-credential-definitions) |
| Participant | provides and consumes data within the MDS, following the MDS Authority's usage policies and data offers vocabulary, and verifying MDS credentials | the [profile](2026/1/mds-2026-1.md), the [ODRL profile](2026/1/policy/mds-odrl-profile-2026-1.md), [Credentials Verification](2026/1/credentials/mds-credentials-2026-1.md#credentials-verification), the [data offers vocabulary](2026/1/vocabulary/mds-vocabulary-2026-1.md) |

The reference connector lives in [`mds-edc`](https://github.com/Mobility-Data-Space/mds-edc).

## Versions

| Version | Specification | Status |
|---|---|---|
| `2026/1` | [`2026/1/mds-2026-1.md`](2026/1/mds-2026-1.md) | DRAFT |

## Layout

The repository mirrors the URI space of the profile, so every published artefact sits at the path its identifier resolves to:

```
2026/1/mds-2026-1.md                                    the profile specification
2026/1/policy/mds-odrl-profile-2026-1.md                ODRL profile specification
2026/1/policy/context.jsonld                            policy JSON-LD context
2026/1/credentials/context.jsonld                       credentials JSON-LD context
2026/1/credentials/mds-credentials-2026-1.md            credential specification
2026/1/credentials/*.schema.json                        credential JSON Schemas
2026/1/vocabulary/mds-vocabulary-2026-1.md              data offers vocabulary specification
2026/1/vocabulary/context.jsonld                        data offers vocabulary JSON-LD context
examples/                                               non-normative examples
```

A future profile version is added as a sibling directory (`2027/1/`, …); published versions are never edited in place.

## Identifiers

Everything is addressed through the [w3id.org](https://w3id.org) namespace `mobility-dataspace`, which redirects to the GitHub Pages site built from this repository. Consumers **MUST** use the `w3id.org` identifiers, never the `github.io` targets — the latter are an implementation detail and may move.

| Identifier | Resolves to |
|---|---|
| `https://w3id.org/mobility-dataspace/2026/1/` | the profile specification |
| `https://w3id.org/mobility-dataspace/2026/1/policy/` | the ODRL profile namespace; resolves to the ODRL profile specification |
| `https://w3id.org/mobility-dataspace/2026/1/policy/context.jsonld` | the policy JSON-LD context |
| `https://w3id.org/mobility-dataspace/2026/1/credentials/` | the credentials vocabulary namespace |
| `https://w3id.org/mobility-dataspace/2026/1/credentials/context.jsonld` | the credentials JSON-LD context |
| `https://w3id.org/mobility-dataspace/2026/1/credentials/<Type>.schema.json` | a credential JSON Schema |
| `https://w3id.org/mobility-dataspace/2026/1/vocabulary/` | the data offers vocabulary namespace; resolves to the data offers vocabulary specification |
| `https://w3id.org/mobility-dataspace/2026/1/vocabulary/context.jsonld` | the data offers vocabulary JSON-LD context |

Context and schema identifiers name documents and redirect with `302`. Namespace identifiers — and the vocabulary terms minted below them, such as `.../policy/ParticipantId` — name concepts rather than documents, so they redirect with `303 See Other` to the specification that describes them.

The redirect rules live in [`perma-id/w3id.org`](https://github.com/perma-id/w3id.org) under `mobility-dataspace/.htaccess`. Changing where an identifier points is a pull request against that repository.
