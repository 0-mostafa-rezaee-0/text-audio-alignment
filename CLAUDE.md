# Project rules

## Goal
A short, practical repo: (1) a README timeline of when forced alignment became usable by an ordinary engineer, (2) one demo notebook that aligns a standard audio clip with its known transcript using the simplest tool available today.

## Scope (do not expand)
- No deep research. The timeline in README.md is already written; only verify the items flagged in the README note.
- Do not install or run old tools (aeneas, Gentle, MFA). Only stable-ts is run.
- Do not add features beyond the demo notebook.

## Working rules
- Work in small steps and report after each: (1) verify flagged years, (2) source the clip, (3) run the notebook.
- The audio clip must be public domain or openly licensed, short (10–30 seconds), clean English speech, with an exact transcript. Record its source and license in `data/SOURCES.md`. Confirm the transcript matches what is actually spoken.
- If something fails after two attempts, record it in `STATUS.md` with the reason and move on. Do not loop on one problem.
- Distinguish fact (confirmed from a source or from running code), inference, and unverified in `STATUS.md`.
- Reproducibility: the environment is `environment.yml` (conda, conda-forge). Create it with `conda env create -f environment.yml` and run everything inside `text-audio-alignment`. Python packages live in `requirements.txt`; `environment.yml` reads it (`pip: - -r requirements.txt`) and adds Python and ffmpeg. If a package must be added or a version pinned, change `requirements.txt` (or `environment.yml` for non-pip items) and note why in `STATUS.md`. If the `-r` line fails in conda, copy the pip packages into `environment.yml` and note it in `STATUS.md`.
- Keep the notebook (`demo.ipynb`) as the single demo. Keep outputs in `outputs/`.
- Do not rewrite the README timeline except to correct a year that you verified; cite the source for any change.
- Commit after each completed step with a short message.
