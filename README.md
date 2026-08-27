# mds-profile

The **Mobility Data Space dataspace profile**: the configuration contract an EDC connector satisfies in order to participate in the MDS.

The connector distribution itself lives in [`mds-edc`](https://github.com/Mobility-Data-Space/mds-edc).

## Versions

| Version | Specification | Status |
|---|---|---|
| `2026/1` | [`2026/1/mds-2026-1.md`](2026/1/mds-2026-1.md) | DRAFT |

## Layout

The repository mirrors the URI space of the profile, so every published artefact sits at the path its identifier resolves to:

```
2026/1/mds-2026-1.md                                    the profile specification
2026/1/policy/context.jsonld                            policy JSON-LD context
2026/1/credentials/context.jsonld                       credentials JSON-LD context
2026/1/credentials/mds-credentials-2026-1.md            credential specification
2026/1/credentials/*.schema.json                        credential JSON Schemas
examples/                                               non-normative examples
```

A future profile version is added as a sibling directory (`2027/1/`, …); published versions are never edited in place.

## Identifiers

Everything is addressed through the [w3id.org](https://w3id.org) namespace `mobility-dataspace`, which redirects to the GitHub Pages site built from this repository. Consumers **MUST** use the `w3id.org` identifiers, never the `github.io` targets — the latter are an implementation detail and may move.

| Identifier | Resolves to |
|---|---|
| `https://w3id.org/mobility-dataspace/2026/1/` | the profile specification |
| `https://w3id.org/mobility-dataspace/2026/1/policy/` | the policy vocabulary namespace |
| `https://w3id.org/mobility-dataspace/2026/1/policy/context.jsonld` | the policy JSON-LD context |
| `https://w3id.org/mobility-dataspace/2026/1/credentials/` | the credentials vocabulary namespace |
| `https://w3id.org/mobility-dataspace/2026/1/credentials/context.jsonld` | the credentials JSON-LD context |
| `https://w3id.org/mobility-dataspace/2026/1/credentials/<Type>.schema.json` | a credential JSON Schema |

Context and schema identifiers name documents and redirect with `302`. Namespace identifiers — and the vocabulary terms minted below them, such as `.../policy/ParticipantId` — name concepts rather than documents, so they redirect with `303 See Other` to the specification that describes them.

The redirect rules live in [`perma-id/w3id.org`](https://github.com/perma-id/w3id.org) under `mobility-dataspace/.htaccess`. Changing where an identifier points is a pull request against that repository.
