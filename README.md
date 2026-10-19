# Does Sign Language Translation Actually Look at the Signer?

Interactive reports on **visual grounding in sign language translation (SLT)** using the How2Sign dataset.
We test whether models' output quality really depends on the signer's body regions (eyes, nose, mouth, face, shoulders, both hands), or whether BLEU gains come from somewhere else.

**Live page:** https://<username>.github.io/<repo>/

---

## Reports

| Report | What it shows |
|---|---|
| [MMSLT Region Ablation (4K Training)](artifacts/mmslt-region-ablation-4k.html) | Blacks out each body region (MediaPipe Holistic landmarks) at test time and re-runs generation with the same checkpoint. The delta shows how much output quality depends on each region. Trained on a 4,000-sentence How2Sign slice; evaluated on 300 test sentences. |
| [Grounding or Guessing](artifacts/grounding-or-guessing.html) | Region-masking reliability of Qwen2.5-VL-3B-Instruct before and after LoRA fine-tuning on 4,000 How2Sign clips. Finding: fine-tuning did not teach the model to look; it made it guess more confidently. |
| [CLIP vs SignCLIP](artifacts/clip-vs-signclip.html) | Cross-check of two zero-shot vision-language scorers on which body region a cue word should ground to. Agreement is 13.6% vs. 13.2% expected by chance (+0.4pp), so neither scorer works as an "independent" reference for the other. |
| [Grounding Example Viewer (4K Training)](artifacts/grounding-viewer-4k.html) | Browse individual examples behind the aggregate numbers. |

## Setup

- **Data:** How2Sign, 4,000-sentence training split (`random4000_v3`), 300 held-out test sentences
- **Scale note:** this is a deliberately small-scale slice, not the full ~31K-sentence set. Scaled-up runs (10K / 20K / ~31K) are planned to test whether grounding improves alongside BLEU as data grows.
- **MMSLT baseline:** best checkpoint at epoch 11 (dev BLEU-4 1.50), test BLEU-4 1.58 from the training log, 1.61 reproduced in this run

## Repository layout

```
.
├─ index.html          # landing page
├─ artifacts/          # self-contained HTML reports
└─ README.md
```

Each report is a single static HTML file and needs no build step. To view locally, open `index.html` in a browser.

## Status

Work in progress. Numbers may change as larger-scale runs finish.

## Data and licensing

How2Sign data is subject to its own license. This repository contains analysis results only; <!-- confirm: no How2Sign videos or frames are redistributed -->.

## Citation / Contact

<!-- Add paper title, authors, and contact once public -->