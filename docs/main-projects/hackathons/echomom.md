---
layout: default
title: EchoMom — Penn Health Hackathon 2025
parent: Hackathons
grand_parent: Main Projects
---

# EchoMom — Penn Health Hackathon 2025

## the problem

Postpartum depression affects 1 in 5 new mothers, but most cases go undetected for months. Current screening relies on in-person questionnaires that require a clinical visit — a barrier many new mothers can't clear in the first weeks after birth. Voice biomarkers offer a non-invasive, accessible alternative.

## what I built

A prototype AI voice screener for postpartum depression, built at Penn Health Hackathon 2025.

- Built a prototype data pipeline integrating voice emotion-recognition models into a HIPAA-aligned clinical workflow
- Designed structured data flows based on FHIR/HL7 standards to simulate integration with healthcare provider systems
- Implemented preprocessing and validation pipelines for voice-based screening signals
- Collaborated with clinicians to translate care-pathway logic into technical system workflows

## how it works

Pipeline: raw voice input → preprocessing (noise reduction, segmentation) → feature extraction (prosody, pitch variance, speech rate) → emotion recognition model → structured output mapped to clinical screening thresholds.

The FHIR/HL7 data flow design was intentional: we wanted the output to be something a real EHR system could actually ingest, not just a standalone demo. This shaped every data structure decision.

## what I learned

Healthcare data has constraints that general ML doesn't. HIPAA alignment isn't a checkbox — it changes how you store intermediate outputs, what you log, and how you structure data flows. Designing for real clinical integration from day one made the system meaningfully different from a toy demo.

Working with clinicians to translate care logic into technical specs was the hardest part. Clinical workflows don't map cleanly to data pipelines.

## screenshots

> 📸 Screenshot: [add when available]

---

**Tech:** Python · Voice ML · NLP · FHIR/HL7 · Pandas
