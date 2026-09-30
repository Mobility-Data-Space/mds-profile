---
---

# MDS Dataspace Profile — 2026/1

> **Status — DRAFT.** This document specifies profile version `2026/1` of the Mobility Data Space dataspace profile. It is not yet released.

## 1. Overview

This profile is the configuration contract an EDC connector satisfies in order to participate in the Mobility Data Space. It bundles:

- the wire protocol — Dataspace Protocol over HTTPS, version `2025-1`;
- the JSON-LD vocabulary for MDS policy terms and the MDS credential model;
- the DCP scopes needed to obtain the credentials MDS relies on;
- the credential model itself, stated normatively;

## 2. Profile identity

| Property | Value |
|---|---|
| Profile id | `mds-2026-1` |
| Protocol version | `2025-1` |
| Protocol binding | `HTTPS` |
| Protocol namespace (DSP) | `https://w3id.org/dspace/2025/1/` |
| Policy namespace | `https://w3id.org/mobility-dataspace/2026/1/policy/` |
| Credentials namespace | `https://w3id.org/mobility-dataspace/2026/1/credentials/` |


## 3. Dataspace profile configuration

```json
{
  "@context": ["https://w3id.org/edc/connector/management/v2"],
  "@type": "DataspaceProfile",
  "name": "mds-2026-1",
  "protocol": {
    "version": "2025-1",
    "binding": "https",
    "namespace": "https://w3id.org/dspace/2025/1/"
  },
  "jsonLdContextsUrl": [
    "https://w3id.org/dspace/2025/1/context.jsonld",
    "https://w3id.org/edc/dspace/v0.0.1",
    "https://w3id.org/mobility-dataspace/2026/1/policy/context.jsonld",
    "https://w3id.org/mobility-dataspace/2026/1/credentials/context.jsonld"
  ]
}
```

## 4. DCP scope

```properties
edc.iam.dcp.scopes.mdsmembership.id=mds-membership
edc.iam.dcp.scopes.mdsmembership.type=DEFAULT
edc.iam.dcp.scopes.mdsmembership.value=org.eclipse.dspace.dcp.vc.type:MembershipCredential:read
edc.iam.dcp.scopes.mdsmembership.profile=mds-2026-1

edc.iam.dcp.scopes.mdsgroupmembership.id=mds-group-membership
edc.iam.dcp.scopes.mdsgroupmembership.type=DEFAULT
edc.iam.dcp.scopes.mdsgroupmembership.value=org.eclipse.dspace.dcp.vc.type:GroupMembershipCredential:read
edc.iam.dcp.scopes.mdsgroupmembership.profile=mds-2026-1
```

## 5. Policy operands

This profile version defines four operands, all in the policy namespace `https://w3id.org/mobility-dataspace/2026/1/policy/`.

| Operand | Operators | Right operand | Source |
|---|---|---|---|
| `ParticipantId` | `eq`, `isAnyOf` | string, or array of strings for `isAnyOf` |`MembershipCredential.credentialSubject.participantId` |
| `Membership` | `eq` | the string `active` | `MembershipCredential.credentialSubject.active` |
| `Group` | `eq`, `isAnyOf`, `isAllOf` | string, or array of strings for `isAnyOf` / `isAllOf` | `GroupMembershipCredential.credentialSubject.groups` |
| `PolicyEvaluationTime` | `eq`, `neq`, `lt`, `lteq`, `gt`, `gteq` | RFC 3339 instant | the runtime clock |

The credentials backing these operands are specified in [MDS Verifiable Credentials — 2026/1](https://w3id.org/mobility-dataspace/2026/1/credentials/).

## 6. Participant DID documents

Each MDS participant is identified by a Decentralized Identifier (DID), whose DID document is resolved by other participants during DCP-based authentication.

### 6.1 Service endpoints

A participant's DID document advertises the services other participants need to reach it, as entries of its `service` array (see [DID Core, §5.4](https://www.w3.org/TR/did-core/#services)).

**Credential Service.** The DID document MUST contain a `service` entry of type `CredentialService`, as required by the [Decentralized Claims Protocol v1.0](https://eclipse-dataspace-dcp.github.io/decentralized-claims-protocol/v1.0/#credential-service-endpoint-discovery). Its `serviceEndpoint` is the base URL of the participant's Credential Service, from which verifiers request the MDS credentials.

**Data Service.** Participants SHOULD publicize each of their connectors in their DID document, following [Discovery of Service Endpoints](https://eclipse-dataspace-protocol-base.github.io/DataspaceProtocol/2025-1/#discovery-of-service-endpoints) in the Dataspace Protocol `2025-1`. In this case:

- the participant MUST add one entry per connector to the `service` array, with the `id`, `type` and `serviceEndpoint` properties;
- the entry's `type` MUST be `DataService`;
- the entry's `serviceEndpoint` MUST be the connector's [version metadata endpoint](https://eclipse-dataspace-protocol-base.github.io/DataspaceProtocol/2025-1/#exposure-of-dataspace-protocol-versions), i.e. the URL ending in `/.well-known/dspace-version`. A consumer resolves the `2025-1` protocol endpoints of the connector from the response of that endpoint.

The following example shows the `service` array of a participant running one connector:

```json
{
  "service": [
    {
      "id": "did:web:identity.mobility-provider.example#credential-service",
      "type": "CredentialService",
      "serviceEndpoint": "https://identity.mobility-provider.example/api/credentials/v1/participants/ZGlkOndlYjppZGVudGl0eS5tb2JpbGl0eS1wcm92aWRlci5leGFtcGxl"
    },
    {
      "id": "did:web:identity.mobility-provider.example#connector-1",
      "type": "DataService",
      "serviceEndpoint": "https://connector.mobility-provider.example/api/dsp/.well-known/dspace-version"
    }
  ]
}
```
