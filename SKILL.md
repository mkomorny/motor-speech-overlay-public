---
name: motor-speech-overlay
description: Generates exhaustive Motor Speech Overlay reports modeling clinical neurogenic and motor-speech variations (spastic, flaccid, ataxic, hypokinetic, hyperkinetic dysarthria, apraxia) as parameter modifiers that interface with core biometric profiles. Trigger with 'motor speech overlay for', 'dysarthria profile of', 'clinical speech modifier for', or '/motor-speech-overlay'.
disable-model-invocation: true
---

# Motor Speech Overlay

## Purpose & Scope

This skill provides a **clinical, neuromotor acoustic modifier layer** that overlays onto the core biometric and personality profiles. When profiling individuals with neurogenic conditions, developmental variations, structural craniofacial differences, or motor-speech disorders (e.g., Down syndrome, Parkinson's disease, post-stroke dysarthria, cerebral palsy), analysts must avoid fork-bombing or reinventing whole new personality/biometric templates. Instead, this skill acts as an authoritative **differential modifier**, adjusting glottal adduction, articulatory precision, resonance leakage, and temporal isochrony.

This skill owns:
- Clinical classification: Flaccid, Spastic, Ataxic, Hypokinetic, Hyperkinetic, or Mixed Dysarthria
- Articulatory imprecision coefficients: vowel centralization, consonant spirantization, cluster simplification
- Velopharyngeal incompetence: hypernasal acoustic leakage area ($	ext{mm}^2$) and nasal emission
- Laryngeal motor control: strained-strangled (hyperadduction) vs. breathy-paralytic (hypoadduction)
- Involuntary motor events: vocal tremor frequency (Hz), dystonic pitch breaks, apraxic groping latencies

This skill does **not** replace the core personality profile (owned by `speaking-personality-profile`) or baseline acoustics (owned by `voice-biometric-profiler`).

---

## Activation Triggers

Activate automatically when:
- User asks for a motor-speech analysis, dysarthria overlay, or clinical voice modification (e.g., *"motor speech overlay for [speaker]"*, *"dysarthria profile of Parkinson's patient"*, *"Down syndrome motor speech modifier"*).
- User triggers `/motor-speech-overlay [subject] [condition]`.
- Simulating speech pathologies, neurological disorders, or developmental articulatory patterns in synthetic voices.
- Pairing clinical speech-language therapy diagnostics with speech synthesis pipelines.

---

## Mandatory Report Schema & Structure

### 1. Clinical Neuromotor Classification & Etiology
- Differential diagnosis: Flaccid, Spastic, Ataxic, Hypokinetic, Hyperkinetic, or Mixed Dysarthria; Childhood Apraxia of Speech (CAS); Craniofacial structural modifications.
- Neuromuscular tone state: Hypotonia (reduced muscle tone) vs. Hypertonia (rigidity/spasticity) vs. Involuntary choreic movements.

### 2. Phonatory & Glottal Dynamics (Laryngeal Subsystem)
- **Adduction Pattern:** Glottal incompetence (hypoadduction / breathiness) vs. hyperfunctional strain (hyperadduction / pressed).
- **Vocal Tremor:** Presence of physiological or pathological tremor (frequency in Hz, modulation depth in % F0/amplitude).
- **Phonatory Stability:** Sudden pitch breaks, voice arrest episodes, or involuntary glottal fry bursts.

### 3. Resonatory Subsystem (Velopharyngeal Function)
- **Hypernasality Index:** Acoustic nasalance percentage (%) and extra nasal formant prominence.
- **Nasal Air Emission:** Audible turbulent friction during high-pressure consonants (/s, z, p, t/).
- **Cul-de-Sac / Pharyngeal Resonance:** Low-frequency pharyngeal trapping due to tongue retraction or macroglossia.

### 4. Articulatory Subsystem (Oral Constriction & Kinematics)
- **Consonant Imprecision:** Spirantization rate of stops (/p, t, k/ realized as fricatives [ɸ, θ, x]); dentalization or interdental protrusion.
- **Vowel Centralization (FCR):** Extent of vowel triangle compression toward schwa.
- **Apraxic Groping / Trial-and-Error Articulation:** Initial consonant search latency (ms) and phoneme re-attempts.

### 5. Prosodic & Respiratory Coordination Subsystem
- **Monopitch & Monoloudness Index:** Standard deviation reduction in F0 and SPL.
- **Short Rushes of Speech:** Sudden acceleration bursts followed by respiratory exhaustion (typical of hypokinesia).
- **Syllable Segregation:** Equal and excess stress on all syllables (ataxic scanning speech).

---

## Machine Output Block

```json
{
  "$schema": "https://json-schemas.voice/motor-speech-overlay.v1.json",
  "speaker_id": "SPEAKER_ID",
  "condition_classification": "DOWN_SYNDROME_HYPOTONIA_MIXED_MOTOR",
  "laryngeal_modifiers": {
    "closed_quotient_modifier": -0.08,
    "jitter_increase_percent": 0.45,
    "shimmer_increase_db": 0.25,
    "hnr_reduction_db": -2.8,
    "intermittent_vocal_fry_rate": 0.28
  },
  "resonatory_modifiers": {
    "velopharyngeal_port_leakage_mm2": 12.0,
    "nasalance_score_percent": 34.0,
    "cul_de_sac_resonance_active": true
  },
  "articulatory_modifiers": {
    "vowel_space_area_compression_ratio": 0.82,
    "stop_spirantization_probability": 0.32,
    "interdental_protrusion_stops": true
  },
  "prosodic_modifiers": {
    "speech_rate_reduction_sps": -0.8,
    "syllable_isochrony_bias": 0.42,
    "respiratory_replenishment_interval_words": 6
  }
}
```

---

## Biometric & Personality Crosswalk

| Motor Modifier | Core Biometric Section | Personality Profile Section | Synthesis Compiler Target |
| :--- | :--- | :--- | :--- |
| Closed Quotient Delta | §1 Glottal Source Characteristics | §1 Executive Summary | Klatt Open Quotient Offset |
| Nasalance Leakage | §3 Resonance Profile | §5.3 Repair Strategies | Nasal Resonator Gain Boost |
| VSA Compression | §3 Formant Frequencies | §5.2 Articulatory Search | Formant Target Centralizer |
| Syllable Segregation | §5 Speaking Rate & Rhythm | §2.5 Repetition & "The Groove" | Syllable Duration Multiplier |

---

## Calibration Reference Example: 30yo Adult Male with Down Syndrome

- **Laryngeal Mechanism:** Mild glottal insufficiency secondary to generalized hypotonia; baseline HNR reduced to 14.5 dB with intermittent low-pitch vocal fry on phrase offsets.
- **Resonatory Profile:** Combined pharyngeal cul-de-sac resonance (due to relative macroglossia and tongue retraction) with mild hypernasality (nasalance ~32%) from variable velopharyngeal closure.
- **Articulatory Precision:** Interdental placement of alveolar stops [t̪, d̪]; stop closure incomplete on 28% of tokens resulting in bilabial spirantization [β].
- **Prosody:** Syllable-timed cadence tendencies (nPVI 44.5); reduced speaking rate (3.4 syllables/second) with frequent respiratory replenishments every 5–7 words.

---

## Generation Rules

1. Formulate the overlay as mathematical deltas and parameter modifiers, never as an isolated disconnect from baseline identity.
2. Ground all articulatory imprecisions in physiological neuromuscular mechanisms (hypotonia, ataxia, rigidity).
3. Every profile must output the machine-readable `motor_speech_modifiers.json` block.
