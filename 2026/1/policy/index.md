---
---

# MDS ODRL Profile — 2026/1

> **Status — DRAFT.** This document specifies the ODRL profile of profile version `2026/1` of the [Mobility Data Space dataspace profile](https://mobility-data-space.github.io/mds-profile/2026/1/). It is not yet released.

## Introduction

This document specifies the MDS ODRL profile: the left operands MDS defines in the namespace `https://w3id.org/mobility-dataspace/2026/1/policy/`, how a policy writes constraints on them, and how a connector evaluates them. Policies are ODRL policies as carried by the Dataspace Protocol 2025-1.

| Operand | Denotes | Evaluated against |
|---|---|---|
| [`Membership`](#membership) | the counterparty is an MDS participant | an MDS MembershipCredential |
| [`ParticipantId`](#participantid) | the counterparty's `did:web` DID | an MDS MembershipCredential |
| [`Group`](#group) | the MDS groups the counterparty belongs to | an MDS GroupMembershipCredential |
| [`EvaluationTime`](#evaluationtime) | the instant of evaluation | the evaluating connector's clock |

## Membership

**IRI:** `https://w3id.org/mobility-dataspace/2026/1/policy/Membership`

### Definition

The counterparty is an MDS participant.

### Constraint

| Operators | Right operand |
|---|---|
| `eq` | the string `active` |

```json
{ "leftOperand": "Membership", "operator": "eq", "rightOperand": "active" }
```

### Evaluation

Permits when the counterparty presents at least one MDS MembershipCredential: a credential that

1. is valid: its proof verifies, it is within its validity period, it is not revoked, and its `credentialSubject.id` is the counterparty's DID;
2. has a `type` that expands to `https://w3id.org/mobility-dataspace/2026/1/credentials/MembershipCredential`: the `type` holds that IRI, or holds `MembershipCredential` with the [MDS credentials context](https://mobility-data-space.github.io/mds-profile/2026/1/credentials/) in its `@context`;
3. is issued by an MDS trusted issuer ([MDS trusted issuers](https://mobility-data-space.github.io/mds-profile/2026/1/)).

A credential of the same type name from any other issuer, including an issuer the connector trusts for another dataspace, is not an MDS MembershipCredential. The type IRI states what a credential claims; the issuer decides whether the claim counts.

A connector **MUST** reject, when the policy is created, a `Membership` constraint with another operator or right operand.

## ParticipantId

**IRI:** `https://w3id.org/mobility-dataspace/2026/1/policy/ParticipantId`

### Definition

The counterparty's participant identifier: its `did:web` DID ([MDS Participant DID Document](https://mobility-data-space.github.io/mds-profile/2026/1/)).

### Constraint

| Operators | Right operand |
|---|---|
| `eq`, `neq` | one DID: a non-empty string without `,` |
| `isAnyOf`, `isNoneOf` | one or more DIDs |

```json
{ "leftOperand": "ParticipantId", "operator": "isAnyOf", "rightOperand": ["did:web:connector.mobility-provider.example", "did:web:operator.example"] }
```

```json
{ "leftOperand": "ParticipantId", "operator": "isNoneOf", "rightOperand": ["did:web:competitor.example"] }
```

### Evaluation

Permits when the counterparty presents an MDS MembershipCredential (see [Membership, Evaluation](#membership)) whose `credentialSubject.id`, which is the counterparty's DID:

- equals the right operand (`eq`), or one of its DIDs (`isAnyOf`);
- differs from the right operand (`neq`), or from all of its DIDs (`isNoneOf`).

`neq` and `isNoneOf` exclude participants from the MDS members; they never permit a counterparty that does not present an MDS MembershipCredential.

A connector **MUST** reject, when the policy is created, a `ParticipantId` constraint with another operator or right operand.

## Group

**IRI:** `https://w3id.org/mobility-dataspace/2026/1/policy/Group`

### Definition

The MDS groups the counterparty belongs to, as issued by MDS.

### Constraint

| Operators | Right operand |
|---|---|
| `eq` | one group identifier: a non-empty string without `,` |
| `isAnyOf`, `isAllOf` | one or more group identifiers |

```json
{ "leftOperand": "Group", "operator": "isAnyOf", "rightOperand": ["parking-operators", "transit-authorities"] }
```

### Evaluation

The counterparty's groups are the `groups` of its MDS GroupMembershipCredential, split on `,`. An MDS GroupMembershipCredential meets the conditions of an MDS MembershipCredential (see [Membership, Evaluation](#membership)), with `https://w3id.org/mobility-dataspace/2026/1/credentials/GroupMembershipCredential` (or `GroupMembershipCredential` with the MDS credentials context) as its type.

Permits when the counterparty belongs to the group (`eq`), to at least one of the groups (`isAnyOf`), or to all of them (`isAllOf`).

A connector **MUST** reject, when the policy is created, a `Group` constraint with another operator or right operand.

## EvaluationTime

**IRI:** `https://w3id.org/mobility-dataspace/2026/1/policy/EvaluationTime`

### Definition

The instant at which the policy is evaluated.

### Constraint

| Operators | Right operand |
|---|---|
| `eq`, `neq`, `lt`, `lteq`, `gt`, `gteq` | one RFC 3339 instant |

```json
{ "leftOperand": "EvaluationTime", "operator": "lt", "rightOperand": "2027-01-01T00:00:00Z" }
```

### Evaluation

Permits when the evaluating connector's clock at evaluation compares with the right operand as the operator states. No credential is involved.

A connector **MUST** reject, when the policy is created, an `EvaluationTime` constraint with another operator or right operand.
