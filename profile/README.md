## Randmesh

Randmesh is an open ecosystem for verifiable and composable randomness systems. It provides a trust-minimized framework for generating, combining, and verifying entropy from multiple sources in a deterministic and auditable workflow model.

The project is structured around a Go-based core library that implements cryptographic primitives, including entropy composition, commit-reveal workflows, and verifiable aggregation of independent randomness sources.

Randmesh is designed for systems where randomness must be verifiable, resistant to manipulation, and auditable. It supports use cases where integrity and traceability of random outputs are more important than strict reproducibility across time.

---

## Core principles

Randmesh does not rely on a single entropy source. Instead, randomness is derived from composable multi-source entropy mixing and verifiable aggregation workflows.

The system is designed under the assumption that at least one entropy source remains unpredictable and uncompromised. Each source is treated as an independent contributor to the final output.

Randmesh does not embed global trust assumptions about external entropy providers and does not guarantee correctness of any application-layer logic consuming generated values.

---

## Cryptographic boundary of guarantees

Randmesh provides cryptographic guarantees strictly within the scope of entropy generation, composition, and verification as defined by its internal specification.

Formally:

* Randmesh guarantees correctness of entropy mixing functions under the defined threat model.
* Randmesh guarantees verifiability of the generation process when accompanied by valid proof artifacts.
* Randmesh guarantees that outputs are derived from the declared entropy sources according to the deterministic composition rules of the system.

Randmesh explicitly does not guarantee:

* reproducibility of outputs over time, since entropy sources may evolve or change their internal state;
* stability of external entropy providers;
* correctness of application-level logic consuming generated values;
* semantic interpretation or filtering applied outside the Randmesh core;
* fairness or integrity of downstream systems using generated outputs.

Any change in entropy source state, availability, or distribution characteristics may result in different outputs for identical requests at different points in time.

---

## Architecture

Randmesh consists of two primary components:

### 1. Core Go library (SDK)

The Randmesh library provides a unified interface for entropy generation and deterministic composition workflows. It supports multiple configurable entropy providers and verifiable aggregation rules.

Some entropy providers may require external API credentials supplied by the user of the library. These credentials are not managed, stored, or proxied by Randmesh and are used exclusively within the local execution context of the application.

Supported entropy sources include:

* cryptographically secure system entropy (`crypto/rand`)
* external randomness APIs using user-provided credentials
* distributed randomness beacons
* blockchain-based entropy signals

Entropy providers are modular and may be added, replaced, or removed without modifying the core system architecture.

---

### 2. Public API service

The Randmesh public API is built exclusively on freely available entropy sources. It does not require external paid credentials and does not rely on user-provided API keys for external services.

The service acts as a reference implementation of verifiable randomness composition over publicly accessible entropy inputs.

---

## Capabilities

Randmesh supports generation of multiple classes of randomness primitives, including:

* integers of a given length
* floating-point numbers
* arbitrary string generation with configurable alphabets
* UUID generation
* byte arrays and binary entropy streams
* cryptographic seeds
* tokens, salts, and nonces

All primitives are derived from the same underlying entropy composition model and can be verified via associated proof structures where applicable.

---

## Use cases

Randmesh is suitable for systems requiring verifiable randomness generation and auditability, including:

* cryptographic key and seed generation
* authentication tokens and session identifiers
* verification codes and one-time values
* deterministic simulations and probabilistic models
* system identifiers and unique resource naming
* audit-critical workflows requiring traceable randomness derivation

---

## Language support

Randmesh is currently implemented as a Go-based reference library providing the canonical implementation of its cryptographic primitives, entropy aggregation model, and verification workflows.

The system is designed to be language-agnostic. While the initial implementation is written in Go, future official language bindings are planned, including a Python SDK distributed via PyPI, with additional implementations under consideration for other ecosystems.

All implementations are intended to conform to a shared specification to ensure consistent behavior, interoperability, and verifiable output semantics across environments.

---

## Design goals

* verifiability of randomness derivation
* composability of entropy sources
* modular provider architecture
* deterministic workflow semantics where applicable
* resistance to single-source entropy compromise
* cross-language specification consistency
* traceable auditability of generation processes
