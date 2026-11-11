# Status

Written but not yet run. Nothing below has been executed.

## Unverified
- The `stable_whisper` calls in `demo.ipynb` (`load_model`, `align`, `save_as_json`, `to_srt_vtt`) were written from memory of the stable-ts API and have not been executed.
- `environment.yml` (python 3.11, conda-forge ffmpeg, pip packages via `-r requirements.txt`) has not been built; the Python version choice is an assumption, and the `-r` line inside the conda pip section is unverified.
- The pip-only path in the README (venv + system ffmpeg) has not been run.
- Years in README: WhisperX (2023) and PyTorch forced alignment API (2024) come from secondary references; the stable-ts release year was not found.

## To do
1. Verify the flagged years from primary sources.
2. Source `data/sample.wav` and `data/sample.txt`; fill in `data/SOURCES.md`.
3. Run `demo.ipynb`, fix API errors, save outputs to `outputs/`.
