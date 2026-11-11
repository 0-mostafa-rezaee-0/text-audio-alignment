# Sources for the demo clip

## Audio: `data/sample.wav`

- **Corpus:** LibriSpeech (Panayotov, Chen, Povey, Khudanpur, ICASSP 2015), `dev-clean` split.
- **Utterance id:** `1272-128104-0002` (speaker 1272, chapter 128104). LibriSpeech is derived from LibriVox audiobook recordings, which are in the public domain (stated on the OpenSLR page). The title of the book was not looked up.
- **Corpus page:** https://www.openslr.org/12/
- **License:** CC BY 4.0 (stated on the OpenSLR page). Redistribution is allowed with attribution; attribution is given here. The underlying LibriVox recordings are public domain.
- **Where this copy was fetched from:** the Hugging Face dataset `hf-internal-testing/librispeech_asr_dummy` (config `clean`, split `validation`, row 2), https://huggingface.co/datasets/hf-internal-testing/librispeech_asr_dummy . This is a small mirror of 73 LibriSpeech dev-clean utterances. The mirror was used for convenience; the audio itself is the LibriSpeech utterance above.
- **Processing:** the mirror served FLAC data. It was converted with `ffmpeg -ac 1 -ar 16000 -c:a pcm_s16le` to 16 kHz mono 16-bit PCM WAV. No trimming; the whole utterance is used.
- **Result:** 12.485 s, 32 words, clean read speech, one speaker. SHA-256 of `sample.wav`: `3165bb4372ed834ddf2dd440e83b8e523b474d3c0eb54951cda81f0ed332505d`.

## Transcript: `data/sample.txt`

- Taken verbatim from the LibriSpeech transcript of the same utterance (upper case, no punctuation), as returned with the audio by the dataset above.

```
HE TELLS US THAT AT THIS FESTIVE SEASON OF THE YEAR WITH CHRISTMAS AND ROAST BEEF LOOMING BEFORE US SIMILES DRAWN FROM EATING AND ITS RESULTS OCCUR MOST READILY TO THE MIND
```

## Does the transcript match the speech?

- **Checked by machine, not by ear.** The clip was transcribed independently with Whisper (`base`, via stable-ts 2.19.1, language `en`) and compared word by word with `sample.txt` after lower-casing and stripping punctuation.
- **Result:** 31 of 32 words are identical. The only difference is "similarly" (Whisper) against "similes" (reference). The reference is the LibriSpeech transcript, and "similes drawn from eating" fits the sentence ("similarly drawn from eating" does not), so the difference is taken to be a Whisper recognition error. This is an inference; it was not confirmed by a human listening to the clip.
- Number of words (32) is the same in both.
