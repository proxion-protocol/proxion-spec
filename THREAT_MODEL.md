# Threat Model

This document outlines the security and privacy threats considered in the design of the Proxion Universal Architecture.

## 1. Honest-but-Curious Coordination Store

**Threat**: The coordination service (if used for store-and-forward) follows the protocol correctly but attempts to learn information about the agents and their communications.
**Impact**: Privacy violation, metadata leakage.
**UI Requirement**:
*   All control messages MUST be end-to-end encrypted.
*   The Store MUST NOT possess keys to decrypt payload content.
*   Agents SHOULD minimize metadata exposure (e.g., using pairwise identifiers).

## 2. Linkability and Correlation

**Threat**: An adversary (network observer or coordination store) correlates multiple identities or sessions to a single real-world entity.
**Impact**: Loss of anonymity, tracking.
**UI Requirement**:
*   Agents SHOULD use distinct keys/identifiers for distinct relationships (Pairwise Identifiers).
*   Protocol headers SHOULD NOT leak global static identifiers.

## 3. Replay and Bearer-Token Attacks

**Threat**: An adversary intercepts a valid Capability token and attempts to use it to gain unauthorized access.
**Impact**: Unauthorized access, impersonation.
**UI Requirement**:
*   Capabilities MUST be bound to a key (Subject).
*   Usage MUST require Proof-of-Possession (PoP) of the bound key (anti-bearer).
*   Requests MUST include nonces or timestamps to prevent simple replay.

## 4. Over-Permission and Privilege Creep

**Threat**: Agents are granted more authority than necessary, or retain authority longer than needed.
**Impact**: Increased blast radius if an agent is compromised.
**UI Requirement**:
*   Capabilities MUST support attenuation (least privilege).
*   Capabilities MUST be short-lived by default.
*   Delegation chains MUST be verifiable.

## 5. Provider Observation

**Threat**: Infrastructure providers (ISP, cloud host) observe traffic patterns.
**Impact**: Traffic analysis.
**UI Requirement**:
*   Transport independence allows for routing over Tor, mixnets, or P2P connections to mitigate this. The spec does not enforce a transport, preventing lock-in to observable centralized transports.

## 6. Revocation Failures

**Threat**: A compromised key or capability cannot be successfully revoked, or revocation information is delayed.
**Impact**: Continued unauthorized access.
**UI Requirement**:
*   Verifiers MUST check revocation status.
*   Revocation propagation latency is an implementation (EI) trade-off, but the mechanism for publishing revocation must be defined.
