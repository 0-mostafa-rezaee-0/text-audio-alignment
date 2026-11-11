# Status

Last updated 2026-11-11. Labels: **fact** = confirmed from a source or from running code; **inference** = reasoned, not directly confirmed; **unverified** = not checked.

## What was run

### Environment (step 0)
- **Fact:** branch is `alignment-demo`, level with `main` (0 commits ahead or behind).
- **Fact:** inside the conda env `text-audio-alignment`: Python 3.11.18, ffmpeg 9.0.2 (from conda), `import stable_whisper` works, stable-ts 2.19.1.
- **Fact:** `conda` is not on PATH in the Bash or PowerShell tools of this session; every command was run through `C:\Users\Mostafa\miniforge3\Scripts\conda.exe run -n text-audio-alignment`. This is a local PATH matter, not a repo problem.
- **Fact (reported by the user, not re-run here):** `conda env create -f environment.yml` succeeded, including the `pip: - -r requirements.txt` line. The env was not rebuilt in this session; it was only inspected. No fallback to copying the pip packages was needed.

### Years in the README (step 1)
- **Fact:** WhisperX is 2023. arXiv 2303.00747, v1 submitted 1 March 2023 (https://arxiv.org/abs/2303.00747). README year kept.
- **Fact:** PyTorch forced alignment API is 2023, not 2024. `torchaudio.functional.forced_align` is absent from the torchaudio 2.0.0 docs (404) and present in the 2.1.0 docs (200); torchaudio 2.0.0 was released 2023-03-15 and 2.1.0 on 2023-10-04 (PyPI). The TorchAudio 2.1 paper (arXiv 2310.17864, 27 Oct 2023) mentions forced alignment tools. README corrected from 2024 to 2023, sources cited.
- **Fact:** stable-ts first PyPI release is 1.0.0 on 2022-11-20 (PyPI release history), latest in the env is 2.19.1 (2025-08-16). README now lists stable-ts under 2022, split off from the "2026 MFA 3.x" row.
- **Unverified:** the year the forced-alignment function (`align`) was added to stable-ts. 2022 is the package's first release, not necessarily the first release that could align to a transcript. This is stated in the README.
- **Unverified:** the other README years (aeneas 2015, Gentle 2016, MFA 2017, MFA 3.x / "today") were not in scope and were not rechecked.

### Clip (step 2)
- **Fact:** `data/sample.wav` is LibriSpeech `dev-clean` utterance `1272-128104-0002`, 12.485 s, 16 kHz mono PCM WAV, 32 words. LibriSpeech is CC BY 4.0 per the OpenSLR page (https://www.openslr.org/12/), so the file is committed. Details and SHA-256 are in `data/SOURCES.md`.
- **Fact:** the copy came from the Hugging Face mirror `hf-internal-testing/librispeech_asr_dummy`; its "wav" URL actually returned FLAC data, which was converted with ffmpeg to real PCM WAV.
- **Fact:** an independent Whisper `base` transcript matches the reference on 31 of 32 words. The one difference is "similarly" against "similes".
- **Inference:** the reference ("similes") is right and Whisper misheard it. Based on the sentence and the LibriSpeech transcript, not on a human listening.
- **Unverified:** nobody has listened to the clip to check the transcript by ear. The title of the source book was not looked up.

### Notebook (step 3)
- **Fact:** `demo.ipynb` ran end to end with `jupyter nbconvert --to notebook --execute` on the first attempt, with no stable-ts API errors. The calls `load_model('base')`, `model.align(..., language='en')`, `save_as_json` and `to_srt_vtt(word_level=True)` all work in 2.19.1.
- **Fact:** `outputs/words.csv`, `outputs/alignment.json` and `outputs/alignment.srt` were written. 32 of 32 words aligned, start times increase, last word ends at 11.86 s of 12.49 s.
- **Change made:** the sanity-check cell only printed values; it now asserts (word count, word order and text, increasing starts, end >= start) and passes. The stale "not yet executed" note in the notebook was updated.
- **Fact:** the word-level `.srt` is karaoke style: one cue per word with the current word wrapped in `<font color>` tags, so cues are repeated. This is how `word_level=True` behaves; the notebook was not changed for it.
- **Inference:** word boundaries look plausible (a pause is found between "year" and "with"; "similes" is long at 1.3 s, probably absorbing trailing silence or stretch). Accuracy was not measured against hand-labelled boundaries.

## Unverified
- The pip-only path in the README (venv + system ffmpeg, no conda) has not been run.
- Behaviour on Linux or macOS, and on GPU, has not been tested. Only Windows 11, CPU.
- Alignment accuracy (no ground-truth word times were available).
- Years listed under "Unverified" above.

## Failures
- None. Nothing needed a second attempt apart from tooling slips (no `conda` on PATH, no `soundfile`/`pyarrow` in the env, `ffprobe` not on the Bash PATH); each was worked around without changing the repo's environment.
