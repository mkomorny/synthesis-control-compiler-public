# Synthesis Control Compiler

> **Tri-Platform Agent Skill** for Claude Desktop / Code, Grok CLI, and Google Antigravity / Gemini.  
> SSML and Neural TTS Parameter Compilation — Compiles complete voice cloning and behavioral dossiers into machine-executable control files: Kokoro blend recipes, SSML tags with viseme/prosody overrides, Praat KlattGrid parameter blocks, and WORLD vocoder recipes.

---

## Overview

`synthesis-control-compiler` provides standardized capabilities across conversational AI platforms:
- Multi-engine target compilation (Kokoro blend recipes, SSML tags, Praat KlattGrid, WORLD).
- Phoneme, pitch contour, and viseme parameter compilation into executable blocks.
- Anti-TTS robotic tone suppression rules and prosodic humanization constraints.
- Standardized compilation bundle packaging (synthesis_controls.json, .ssml, .klatt).
- LLM persona system prompt compilation with pronunciation rules.
- Tri-platform NTFS junctions connecting Claude, Grok, and Antigravity.
- Standard documentation suite: SKILL.md, HOW_TO_USE.txt, IMPLEMENTATION_PLAN.md, and README.md.

---

## Tri-Platform Architecture

Zero duplicate code across platforms. Canonical source resides in `.agents`:
- **Canonical Source**: `C:\Users\<you>\.agents\skills\synthesis-control-compiler`
- **Claude**: `C:\Users\<you>\.claude\skills\synthesis-control-compiler` (NTFS Junction)
- **Grok**: `C:\Users\<you>\.grok\skills\synthesis-control-compiler` (NTFS Junction)
- **Antigravity**: `C:\Users\<you>\.gemini\config\skills\synthesis-control-compiler` (NTFS Junction)

---

## Documentation Suite

- [`HOW_TO_USE.txt`](HOW_TO_USE.txt): Standardized user guide and prompt templates.
- [`IMPLEMENTATION_PLAN.md`](IMPLEMENTATION_PLAN.md): Feature checklist and roadmap.
- [`App Changes Tracker.html`](App%20Changes%20Tracker.html): Interactive visual version log.
- [`SKILL.md`](SKILL.md): Agent system instructions and triggers.
