# M-PPS v1.1 — Release Declaration

## Overview
Modular Personal Productivity System (M-PPS) specification v1.1.  
This release follows the Protocol Release Guide v1.0.

## Verification Metadata
- SHA-256 (spec.md): `e0881bbf6a26140e58d399fd45a46e3be989940b5d852bf6c68aacf0c5d031ba`
- DID (author): did:key:z6Mkff71g8KC2qxWegsCwDYsnCMMtH7AcYNcuUcbVTNL53NC
- Git tag: `m-pps/v1.1`
- Proof source: `/Users/susanfeltner/Documents/Proofs/M-PPS-v1.1/M-PPS-Specification v1.1.md`

## Directory Structure
```
protocols/m-pps/v1.1/
├─ spec.md
├─ schema.json
├─ examples/
│  └─ README.md
└─ proof.ref.json
releases/m-pps/checksums/
└─ v1.1.txt
```

## Compatibility Notes
- Based on: v1.0 (conceptual)
- Backward compatibility: true (no breaking field rename)
- Notes: Structural clarifications and schema placeholder included.

## DID & Hash
- DID binds authorship to the signed specification hash.
- Recompute: `shasum -a 256 protocols/m-pps/v1.1/spec.md`
- Expected: `e0881bbf6a26140e58d399fd45a46e3be989940b5d852bf6c68aacf0c5d031ba`
