# Proxion Glossary (TERMS.md)

This document defines the neutral terminology used within the Universal Architecture.

## A
*   **Agent**: An autonomous entity (software or hardware) capable of holding cryptographic keys and acting on its own behalf.
*   **Attenuation**: The process of creating a new Capability with a subset of the permissions of the original.

## C
*   **Capability**: An unforgeable token that grants specific authority to a Subject on a Resource.
*   **Caveat**: A restriction or condition added to a Capability (e.g., "read-only", "expires in 5 minutes").
*   **Coordination Store**: An abstract service that holds encrypted messages for asynchronous delivery.

## D
*   **Delegation**: The act of an Agent transferring a subset of its authority to another Agent via a Capability.

## E
*   **Existential Instantiation (EI)**: A concrete implementation of the Universal Architecture using specific technologies (e.g., TCP/IP, Ed25519).

## H
*   **Honest-but-Curious**: A trust model where a participant (e.g., the Store) is trusted to follow the protocol but assumed to analyze all available data for intelligence.

## I
*   **Issuer**: The Agent that signs and creates a Capability.

## P
*   **Pairing**: The process of establishing a trust relationship between two Agents.
*   **Proof-of-Possession (PoP)**: A cryptographic challenge-response mechanism proving that the presenter of a Capability holds the private key associated with the Subject.

## R
*   **Resource**: An abstract entity (file, service, device) access to which is controlled by the system.
*   **Revocation**: The act of invalidating a Capability before its natural expiration.

## S
*   **Subject**: The entity to whom authority is granted in a Capability.

## U
*   **Universal Instantiation (UI)**: The abstract, normative specification of the system, independent of implementation details.

## W
*   **Witness**: A concrete technology or system that proves the viability of the UI (e.g., "WireGuard is a witness for the Transport abstraction").
