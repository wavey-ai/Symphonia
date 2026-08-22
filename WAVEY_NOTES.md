# Wavey fork notes

This fork exists to provide a pure-Rust AAC decoder with HE-AAC v1/v2 support
to SoundKit while the upstream work in
[pdeljanov/Symphonia#473](https://github.com/pdeljanov/Symphonia/pull/473)
is still under review.

`main` contains the tested HE-AAC implementation from that pull request. The
later upstream 0.6.1 line is retained as `upstream-0.6.1`; its AAC API refactor
conflicts substantially with the SBR/PS patch and still needs a deliberate
port rather than a mechanical conflict resolution.

Validation recorded in SoundKit on 2026-08-22:

- `cargo test -p symphonia-codec-aac`: 101 tests passed;
- FFmpeg differential HE-AAC fixture: 68.59 dB SNR, zero-frame alignment;
- FFmpeg differential AAC-LC fixtures: 75.45-80.56 dB SNR across M4A, MP4,
  fragmented MP4, MOV, and Matroska;
- MPEG-TS MP2 through `symphonia-bundle-mp3`: 50.36 dB SNR.

SoundKit follows this repository's `main` branch rather than a commit pin.
Before rebasing or merging upstream 0.6.x API changes into `main`, rerun the
SoundKit FATE and collected-media manifests so AAC-LC, HE-AAC, and MP2 quality
cannot silently regress.
