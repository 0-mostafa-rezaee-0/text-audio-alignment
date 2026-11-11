# Text–Audio Forced Alignment

**Task:** given an audio recording and its transcript, return the start and end time of each word (or phone).

This repo has two parts:

1. A short **timeline** of when forced alignment became usable by an ordinary engineer.
2. A **demo notebook** that aligns one standard audio clip with its known transcript using the simplest tool available today.

## Perspective

The timeline is written from the point of view of an engineer who can pull a public library onto a laptop and integrate it into their own pipeline. Research-only systems, proprietary products and tools that needed specialist setup are left out. Dates are the earliest evidence of public availability that we found.

## Timeline: when could an engineer use this?

| Year | Tool | How an engineer would use it |
|------|------|------------------------------|
| 2015 | aeneas | `pip install`, command line or Python library; output is a sync map |
| 2016 | Gentle | Docker image or Mac app; REST API and command line; JSON output; English only |
| 2017 | Montreal Forced Aligner (MFA) | Stand-alone Kaldi-based package; word and phone boundaries; trainable on own data |
| 2023 | WhisperX | Python; Whisper-based transcription plus word-level alignment |
| 2024 | PyTorch forced alignment API | GPU-accelerated Viterbi alignment inside PyTorch |
| 2026 | MFA 3.x, stable-ts | Current MFA release; stable-ts aligns audio to a given transcript |

### Before 2015
Forced aligners existed but were built for phonetics research. The common ones (Prosodylab-aligner, P2FA, FAVE, MAUS) rely on the HTK toolkit. They are mentioned for context only and are not part of the timeline.

### 2015: aeneas
- Source code was published on GitHub in May 2015.
- Install: `pip install numpy`, then `pip install aeneas`. It needs `espeak`, `ffmpeg` and `ffprobe` on the PATH.
- Designed for users with no speech-processing knowledge; ships a command-line tool (`execute_task`) and a Python/C library.
- Input is an audio file plus a text file split into fragments. Output is a synchronization map.
- Debian was the only officially supported OS; other Linux distributions, macOS and Windows were reported to work.

### 2016: Gentle
- Kaldi-based aligner; version 0.9.1 was already cited in May 2016.
- Three ways to run it: Mac application, Docker image, or source.
- Integration: a local REST API (`localhost:8765`) or a command line (`python3 align.py audio.mp3 words.txt`), with JSON output.
- English only. Users reported that installing from source was difficult.

### 2017: Montreal Forced Aligner
- Presented at Interspeech 2017 as the successor to Prosodylab-aligner, using Kaldi instead of HTK.
- Triphone acoustic models and speaker adaptation; trainable on new data.
- Distributed as a stand-alone package; aligns word and phone boundaries.
- Today pretrained models are available for many languages.

### 2023–2024: neural aligners
- WhisperX (2023) adds word-level timestamps to Whisper transcripts using a separate alignment model.
- PyTorch's forced alignment API implements GPU-accelerated Viterbi alignment (described in 2024 work).

### Today (November 2026)
- MFA is at version 3.x and still maintained.
- stable-ts can force-align audio to a given transcript. This is the approach used in the demo.

> **To verify before publishing:** the 2023 (WhisperX) and 2024 (PyTorch API) years come from secondary references, and the stable-ts release year was not found. See `STATUS.md`.

## Demo

`demo.ipynb` aligns one short public-domain clip (`data/sample.wav`) with its known transcript (`data/sample.txt`) using stable-ts and prints the start and end time of every word. Outputs are written to `outputs/`.

The environment is defined in `environment.yml` (conda) so anyone can reproduce it:

```bash
conda env create -f environment.yml
conda activate text-audio-alignment
jupyter lab demo.ipynb
```

`ffmpeg` is installed by conda; no other system dependency is needed.

Prefer plain pip? Use Python 3.11, install `ffmpeg` yourself (e.g. `apt install ffmpeg` or `brew install ffmpeg`), then:

```bash
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
jupyter lab demo.ipynb
```

`requirements.txt` is the single list of Python packages; `environment.yml` reads it and adds Python and ffmpeg.

## Repo structure

```
text-audio-alignment/
├── README.md          # this file: timeline + demo
├── CLAUDE.md          # rules for Claude Code
├── STATUS.md          # what was run, what failed, what is unverified
├── requirements.txt   # Python packages (pip)
├── environment.yml    # conda environment: python, ffmpeg + requirements.txt
├── demo.ipynb
├── data/
│   ├── sample.wav     # not committed until sourced
│   ├── sample.txt     # exact transcript of the clip
│   └── SOURCES.md     # where the clip and transcript came from, license
└── outputs/           # aligned words (json, srt)
```

## Sources
- aeneas: https://github.com/readbeyond/aeneas and https://www.albertopettarin.it/blog/2016/08/03/inside-aeneas-part-1-motivation-and-design-principles.html
- Gentle: https://github.com/strob/gentle (version cited in the MFA poster: https://montreal-forced-aligner.readthedocs.io/en/v1.0/_downloads/c08c0a663da831c22b71fa189af85c9d/MFA_poster_LSA2017.pdf)
- MFA paper: https://www.isca-archive.org/interspeech_2017/mcauliffe17_interspeech.html
- MFA user guide (other tools, current version): https://montreal-forced-aligner.readthedocs.io/en/latest/user_guide/
- easytranscriber (WhisperX, PyTorch alignment API): https://pypi.org/project/easytranscriber/
- stable-ts alignment: https://awesome.ecosyste.ms/projects/github.com%2Fcrone-ai%2Fforce-align-wordstamps
