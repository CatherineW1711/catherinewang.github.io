---
layout: default
title: EchoMom — Penn Health Hackathon 2025
parent: Hackathons
grand_parent: Main Projects
---

# EchoMom — Penn Health Hackathon 2025
## The problem

Postpartum depression affects 1 in 7 new mothers, but most cases go undetected for months. Current screening relies on in-person questionnaires that require a clinical visit — a barrier many new mothers, particularly those in rural areas or on Medicaid, can't clear in the first weeks after birth. Voice biomarkers offer a non-invasive, accessible alternative.

## What we built

A prototype AI voice screener for postpartum depression, built at Penn Health Hackathon 2025.

- Built a prototype data pipeline integrating voice emotion-recognition models into a HIPAA-aligned clinical workflow
- Designed structured data flows based on FHIR/HL7 standards to simulate integration with EHR systems (Epic, Cerner)
- Implemented preprocessing and validation pipelines for voice-based screening signals, including prosodic features (MFCCs, pitch dynamics, zero crossing rate) informed by clinical literature on vocal biomarkers for depression
- Prototyped a clinician-facing dashboard with risk score visualization and automated referral pathways
- Collaborated with clinicians to translate care-pathway logic into technical system workflows

## How it works

Pipeline: raw voice input → preprocessing (noise reduction, normalization, feature extraction — MFCCs, pitch variance, speech rate) → multimodal fusion (acoustic features + BERT-based sentiment from transcribed text + EHR data) → risk scoring model (logistic regression / random forest) → structured output mapped to clinical screening thresholds (low / medium / high), pushed to EHR via SMART on FHIR.

The FHIR/HL7 data flow design was intentional: we wanted the output to be something a real EHR system could actually ingest, not just a standalone demo. This shaped every data structure decision.

## What I learned

Healthcare data has constraints that general ML doesn't. HIPAA alignment isn't a checkbox — it changes how you store intermediate outputs, what you log, and how you structure data flows. Designing for real clinical integration from day one made the system meaningfully different from a toy demo.

Working with clinicians to translate care logic into technical specs was the hardest part. Clinical workflows don't map cleanly to data pipelines — and equity considerations (language support, offline capability, demographic bias in training data) have to be built in from the start, not added later.

---

## Screenshots

![alt text](<Screenshot 2026-03-15 at 10.09.56 PM.png>)
![alt text](<Screenshot 2026-03-15 at 10.10.03 PM.png>)
![alt text](<Screenshot 2026-03-15 at 10.10.12 PM.png>)

---

## Presentation Slide
https://www.dropbox.com/scl/fi/ubkpf4fraa62k18np5fko/EchoMom-1.pdf?rlkey=kbrrkzh3v64s5ecibd70rwwbg&st=icczar9n&dl=0

**Tech:** Python · Voice ML · NLP (BERT, wav2vec 2.0) · FHIR/HL7 · React · AWS
