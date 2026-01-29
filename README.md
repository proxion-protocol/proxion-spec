# Proxion: Universal Architecture (UI)

> **Normative Specification**

This repository defines the **Universal Architecture (UI)** for Proxion: an open, privacy-preserving coordination and delegation control plane.

## Purpose

The Universal Architecture (UI) defines the abstract rules, data structures, and behaviors required for secure pairing, delegation, capability attenuation, revocation, and usage control. It provides a formal basis for coordination between agents and devices without relying on a central authority.

This specification is **universal**: it must be possible for multiple, mutually incompatible implementations (Existential Instantiations, or EI) to conform to this spec.

## Core Problem Statement

Proxion addresses the following problems in a transport- and identity-agnostic way:

*   **Pairing**: Establishing trust between two disjoint agents without prior shared secrets.
*   **Delegation**: Attenuating and transferring authority from one agent to another.
*   **Revocation**: Invalidation of capabilities before their natural expiry.
*   **Coordination**: Enabling asynchronous message passing and state synchronization without a trusted central bus.

## Universal (UI) vs. Existential (EI)

*   **Universal Instantiation (UI)**: The set of all true statements about the system that hold regardless of implementation. This repository contains the UI.
*   **Existential Instantiation (EI)**: A concrete system that witnesses the UI. Example: "There exists a system using WireGuard and VS Code that satisfies Proxion."

## Non-Goals & Independence

To ensure universality, this specification intentionally excludes:

*   **Mandatory Identity System**: No requirement for DID, OIDC, X.509, or any specific PKI.
*   **Mandatory Transport**: No requirement for HTTP, WebRTC, WebSocket, or Bluetooth.
*   **Mandatory Coordination Backend**: No requirement for a specific relayed service, DHT, or blockchain.
*   **Application Coupling**: No assumptions about the nature of the application (e.g., chat, file transfer, SSH).

> **Note**: Technologies like Solid, DIDs, UMA, WireGuard, and WebRTC are considered possible **witnesses** (EI), not requirements.

## Licensing

Licensed under the Apache License, Version 2.0.
