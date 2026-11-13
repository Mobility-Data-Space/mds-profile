---
---

# MDS ODRL Profile — 2026/1

> **Status — DRAFT.** This document specifies the ODRL profile of profile version `2026/1` of the [Mobility Data Space dataspace profile](https://mobility-data-space.github.io/mds-profile/2026/1/). It is not yet released.

## Introduction

This document specifies the MDS ODRL profile: the left operands MDS defines in the namespace `https://w3id.org/mobility-dataspace/2026/1/policy/`, how a provider writes constraints on them, and how a participant's connector evaluates them. Policies are ODRL policies as carried by the Dataspace Protocol 2025-1.

| Operand | Denotes | Evaluated against |
|---|---|---|
| [`Membership`](#membership) | the counterparty is an MDS participant | an MDS MembershipCredential |
| [`ParticipantId`](#participantid) | the counterparty's `did:web` DID | an MDS MembershipCredential |
| [`Group`](#group) | the MDS groups the counterparty belongs to | an MDS GroupMembershipCredential |
| [`EvaluationTime`](#evaluationtime) | the instant of evaluation | the evaluating connector's clock |

### Constraints outside this profile

A connector **MUST** evaluate as not satisfied a constraint whose left operand is in `https://w3id.org/mobility-dataspace/2026/1/policy/` and that does not follow this profile: an operand other than the four above, or an operator or right operand the operand does not allow.

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

**Credential binding:** MDS MembershipCredential, `https://w3id.org/mobility-dataspace/2026/1/credentials/MembershipCredential`. Its presence is evaluated; no claim is read.

A connector **MUST** evaluate a `Membership` constraint as satisfied when, and only when, the counterparty presents an MDS MembershipCredential.

## ParticipantId

**IRI:** `https://w3id.org/mobility-dataspace/2026/1/policy/ParticipantId`

### Definition

The counterparty's participant identifier: its `did:web` DID ([Participant DID document](https://mobility-data-space.github.io/mds-profile/2026/1/#a-participant-did-document)).

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

**Credential binding:** MDS MembershipCredential, `https://w3id.org/mobility-dataspace/2026/1/credentials/MembershipCredential`.

A connector **MUST** evaluate a `ParticipantId` constraint as satisfied when, and only when, the counterparty presents an MDS MembershipCredential whose `credentialSubject.id`:

- equals the right operand (`eq`), or one of its DIDs (`isAnyOf`);
- differs from the right operand (`neq`), or from all of its DIDs (`isNoneOf`).

`neq` and `isNoneOf` exclude participants from the MDS members. A connector **MUST NOT** evaluate a `neq` or `isNoneOf` constraint as satisfied for a counterparty that does not present an MDS MembershipCredential.

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

**Credential binding:** MDS GroupMembershipCredential, `https://w3id.org/mobility-dataspace/2026/1/credentials/GroupMembershipCredential`, split on `,`.

A connector **MUST** evaluate a `Group` constraint as satisfied when, and only when, the counterparty presents an MDS GroupMembershipCredential whose `groups` include the group (`eq`), at least one of the groups (`isAnyOf`), or all of them (`isAllOf`).

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

**Credential binding:** none. The evaluating connector's clock at evaluation is read.

A connector **MUST** evaluate an `EvaluationTime` constraint as satisfied when, and only when, its clock at evaluation compares with the right operand as the operator states.
