# Proxion Specification (UI)

## Status
**Draft 0.1** - Universal Architecture

## 1. Introduction

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in BCP 14 [RFC2119] [RFC8174] when, and only when, they appear in all capitals, as shown here.

This specification defines the syntax and semantics of the Proxion Control Plane using predicate logic and abstract data types.

## 2. Agents, Keys, and Identifiers

### 2.1 Agents
An **Agent** is an autonomous entity capable of holding secrets and signing messages.
*   **Axiom**: For every Agent `A`, there exists a set of cryptographic key pairs `K_A`.
*   **Constraint**: An Agent MUST be uniquely identified by a public key or a determinstic derivation thereof.

### 2.2 Unlinkability
*   **Requirement**: Agents SHOULD use pairwise-unique identifiers when interacting with different peers to prevent correlation by an observer.

## 3. Capabilities

A **Capability** is a portable, unforgeable token of authority.

### 3.1 Structure
A Capability `C` MUST contain:
*   `Issuer`: The Agent granting the authority.
*   `Subject`: The Agent (or public key) acting as the beneficiary.
*   `Resource`: The abstract resource being targeted.
*   `Action`: The permitted operation.
*   `Caveats`: A set of extensive restrictions (attenuation).
*   `Signature`: A cryptographic signature by the `Issuer`.

### 3.2 Finite Lifetime
*   **Requirement**: All Capabilities MUST have a finite lifetime (`NotBefore` and `NotAfter`).
*   **Constraint**: Infinite-lived capabilities are invalid.

### 3.3 Proof-of-Possession
*   **Requirement**: The system MUST implement Proof-of-Possession (PoP) to prevent bearer-token theft.
*   **Mechanism**: The `Subject` MUST sign a challenge to exercise the Capability. Mere possession of the token bits is insufficient for authorization.

## 4. Delegation and Attenuation

### 4.1 Delegation
Any Agent possessing a valid Capability `C` MAY issue a new Capability `C'` if:
*   `C`.Subject == `C'`.Issuer
*   `C'`.Resource is a subset of `C`.Resource
*   `C'`.Caveats is a superset of `C`.Caveats (monotonic attenuation)
*   The valid time range of `C'` is within the range of `C`.

### 4.2 Attenuation
Attenuation acts as an intersection of permissions. A derived capability CANNOT grant more authority than the parent capability.

## 5. Usage Control

Usage control extends beyond simple Access Control by imposing conditions on *how* data is used after access is granted.

*   **Requirement**: The specification supports conditional grants based on verifiable predicates (e.g., "Delete after 24h", "Audit logging required").

## 6. Revocation

### 6.1 Semantics
Revocation is the premature termination of a Capability's validity.
*   **Mechanism**: Issuers MUST support a revocation registry or signaling mechanism.
*   **Constraint**: A Verifier MUST check the revocation status of the entire delegation chain.

## 7. Coordination Store

The **Coordination Store** is an honest-but-curious abstract service used for asynchronous mailboxing.
*   **Requirement**: The Store MUST NOT be able to read the plain text of control messages.
*   **Requirement**: The Store MUST enforce rate limiting and storage quotas.
*   **Assumption**: The Store MAY observe access patterns (metadata) unless obscured by a mixnet (EI choice).

## 8. Authorization Logic
Access is granted if and only if:
1.  A valid chain of Capabilities exists from the Resource Owner to the Requestor.
2.  Every Capability in the chain is valid (signature correct, unexpired, unrevoked).
3.  All Caveats in the chain are satisfied by the request context.
4.  The Requestor proves possession of the Subject key.

