---
name: synthesis-control-compiler
description: Compiles the full voice cloning and behavioral dossier into machine-executable control files: Kokoro blend recipes, SSML tags with viseme/prosody/phoneme overrides, Praat KlattGrid parameter blocks, WORLD vocoder recipes, and LLM persona system prompts with anti-TTS rules. Trigger with 'compile voice synthesis for', 'generate TTS recipe for', 'build synthesis controls for', or '/synthesis-compiler'.
disable-model-invocation: true
---

# Synthesis Control Compiler

## Purpose & Scope

This skill is the **operational compiler** that translates qualitative and quantitative reports into exact machine instructions for speech synthesis engines. Without this skill, voice profiling produces descriptive literature; with this skill, dossiers compile directly into executable configuration blocks for Kokoro, SSML-compliant engines, Praat KlattGrid parametric synthesizers, WORLD vocoders, and LLM persona generators.

This skill owns:
- Kokoro TTS blend recipes (model identifiers, linear weighting coefficients, speed scalars, IPA fixes)
- Compliant SSML markups with `<phoneme>`, `<prosody>`, and `<break>` tags derived from idiolect
- Praat KlattGrid script blocks defining F0, F1–F4, B1–B4, OQ, and AV tracks
- WORLD vocoder matrix configurations (F0 pitch tier, spectral envelope, aperiodicity floor)
- LLM persona prompting guidelines containing strict **anti-TTS negative constraints**

This skill does **not** generate original raw acoustic measurements (compiled from other skills).

---

## Activation Triggers

Activate automatically when:
- User asks to compile synthesis files, generate a TTS recipe, or build voice clone configs (e.g., *"compile synthesis controls for [subject]"*, *"build Kokoro recipe for [voice]"*).
- User triggers `/synthesis-compiler [subject]`.
- User asks: *"How do I actually make this voice speak?"* or *"Give me the machine files for this clone."*
- Exporting Praat scripts, SSML markup, or LLM prompting directives from a completed voice dossier.

---

## Mandatory Report Schema & Structure

### 1. Target Engine Matrix & Routing
- Engine suitability assessment (Kokoro, ElevenLabs, VITS, Praat Klatt, WORLD, Edge-TTS).
- Strengths, known engine artifacts, and architectural limits for this specific speaker profile.

### 2. Kokoro Voice Blend Recipe
- Base voice model selections (e.g., `am_adam`, `am_michael`, `am_george`, `af_bella`).
- Exact mathematical blend weights (summing to 1.00).
- Playback speed scalar (e.g., 0.94x) and language code.
- Pronunciation workaround dictionary for Kokoro phonemizer limitations.

### 3. Standards-Compliant SSML Specification
- Custom SSML text snippet demonstrating exact mapping of idiolectal vowels (`<phoneme alphabet="ipa" ph="...">`), emphatic pitches (`<prosody contour="...">`), and pauses (`<break time="...ms"/>`).

### 4. Praat KlattGrid Parameter Block
- Formant frequency tracks (F1, F2, F3, F4 in Hz) and bandwidths (B1, B2, B3, B4 in Hz).
- Glottal voicing parameters: Open Quotient (OQ %), Voicing Amplitude (AV in dB), Aspiration Amplitude (AH in dB).
- Time-series pitch points (Time s, F0 Hz).

### 5. WORLD Vocoder Resynthesis Recipe
- Target F0 contour scaling parameters.
- Spectral envelope (`sp`) warping coefficients (formant shifting / vocal tract length scaling).
- Aperiodicity (`ap`) noise floor modifier for roughness and breathiness injection.

### 6. LLM Persona Prompt & Anti-TTS Constraints
- System instructions for dialogue generators (text style, disfluency insertion rates, phrase lengths).
- **Forbidden Generic-TTS Habits:** Explicit negative constraints forbidding standard AI assistant tropes (e.g., forbidding *"certainly!"*, balanced antithesis, smooth transitions, robotic neutral cadence).

---

## Machine Output Block

```json
{
  "$schema": "https://json-schemas.voice/synthesis-compiler.v1.json",
  "speaker_id": "SPEAKER_ID",
  "kokoro_recipe": {
    "base_voices": [
      {"id": "am_adam", "weight": 0.65},
      {"id": "am_george", "weight": 0.35}
    ],
    "speed": 0.96,
    "lang": "en-us",
    "lexicon_fixes": {
      "huge": "yooje",
      "coffee": "cawfee"
    }
  },
  "klattgrid_constants": {
    "open_quotient": 0.44,
    "flutter": 0.08,
    "amplitude_voicing_db": 62,
    "amplitude_aspiration_db": 18,
    "f1_b1": [580, 90],
    "f2_b2": [920, 110],
    "f3_b3": [2350, 140],
    "f4_b4": [3450, 220]
  },
  "world_parameters": {
    "f0_floor_hz": 80,
    "f0_ceil_hz": 280,
    "vtl_warp_factor": 1.04,
    "aperiodicity_boost_db": 2.5
  },
  "llm_negative_constraints": [
    "NEVER use introductory polite fillers ('Sure thing', 'Certainly', 'As an AI')",
    "NEVER produce grammatically balanced compound clauses connected by 'moreover' or 'furthermore'",
    "Enforce 1 rhetorical question per 3 declarative turns",
    "Insert signature parenthetical aside every 4th turn with pitch drop"
  ]
}
```

---

## Biometric & Personality Crosswalk

| Compiler Parameter | Core Biometric Section | Personality Profile Section | Source Satellite Skill |
| :--- | :--- | :--- | :--- |
| Kokoro Weights | §1 Mean F0 & §3 Spectral Tilt | §1 Executive Summary | `affect-register-atlas` |
| SSML `<break>` | §5 Pause & Phrasing | §5.1 Turn-Taking Cadence | `temporal-pause-breath-architecture` |
| SSML `<phoneme>` | §6 Vowel & Consonant Features | §3.3 Lexical Profile | `idiolect-phonetic-atlas` |
| KlattGrid OQ/AV | §1 Glottal Closed Quotient | §4.1 Dominant Attitude | `articulatory-vocal-tract-geometry` |
| Anti-TTS Prompts | §8 Intra-Speaker Variability | §2 Core Personality Traits | `disfluency-repair-grammar` |

---

## Calibration Reference Example: Queens Orator Baseline

- **Kokoro Blend:** `am_adam` (0.65) + `am_george` (0.35) @ 0.94x speed provides gruff baritone resonance with nasal forward placement.
- **SSML Sample:**
  ```xml
  <speak>
    We are going to win, folks. <break time="850ms"/>
    And it is going to be <prosody contour="(0%,+0st) (40%,+6st) (100%,-2st)">
    <phoneme alphabet="ipa" ph="juːdʒ">huge</phoneme></prosody>.
  </speak>
  ```
- **Klatt Parameterization:** OQ set to 0.42 (pressed modal); AV at 64 dB; cascade branch enabled with nasal zero at 1800 Hz and nasal pole at 2100 Hz to emulate nasal twang.

---

## Generation Rules

1. Every compilation must deliver functional Kokoro recipe parameters, compliant SSML tags, and Praat/WORLD numerical matrices.
2. Always formulate actionable LLM negative prompting constraints to block generic assistant dialogue.
3. Every profile must output the complete machine-readable `compiler_output.json` block.
