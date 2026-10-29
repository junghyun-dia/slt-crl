# Does Sign Language Translation Actually Look at the Signer?

Interactive reports on **visual grounding in sign language translation (SLT)** across American Sign Language (How2Sign, WLASL) and Korean Sign Language (NIKL Korean Sign Language Corpus).
We test whether models' output quality really depends on the signer's body regions (eyes, nose, mouth, face, shoulders, both hands), or whether BLEU gains come from somewhere else.

**Live page:** [https://junghyun-dia.github.io/slt-crl/](https://junghyun-dia.github.io/slt-crl/)
**Live demo:** [https://6860aqq1pz1upy-5173.proxy.runpod.net/](https://6860aqq1pz1upy-5173.proxy.runpod.net/)
**Demo video:** [https://youtu.be/FLVSBz9HGCQ](https://youtu.be/FLVSBz9HGCQ)

---

## Datasets

| Dataset | Language | Unit | Used for |
|---|---|---|---|
| [How2Sign](https://how2sign.github.io/) | ASL → English | Sentence | SLT training and all grounding reports below (4,000-sentence training slice, 300 test sentences) |
| [WLASL](https://dxli94.github.io/WLASL/) | ASL | Isolated word | Initial probing of how well vision-language models understand body-region information. Not used to train any SLT model. |
| NIKL Korean Sign Language Corpus 2023, 2024 (국립국어원 한국수어 말뭉치) | KSL → Korean | Sentence | SLT training and the demo |

**NIKL** stands for the National Institute of Korean Language (국립국어원). We use the NIKL Korean Sign Language Corpus 2023 and 2024 with approval from NIKL, covering use for AI model training and presentation at academic conferences and in publications, including this public project page and demo prepared for that presentation. The corpus itself is not redistributed in this repository.

## Demo

A conversation between a Deaf and a hearing participant in **Korean Sign Language**, in which the Deaf signer takes part directly in finalizing the translation. It shows the **Conversational Repair Loop** in action, using a model trained on the NIKL Korean Sign Language Corpus.

[![Demo video](https://img.youtube.com/vi/FLVSBz9HGCQ/maxresdefault.jpg)](https://youtu.be/FLVSBz9HGCQ)

- **Video:** [youtu.be/FLVSBz9HGCQ](https://youtu.be/FLVSBz9HGCQ)
- **Try it live:** [6860aqq1pz1upy-5173.proxy.runpod.net](https://6860aqq1pz1upy-5173.proxy.runpod.net/) (hosted on a RunPod instance, so it may be offline at times)

## Reports

| Report | What it shows |
|---|---|
| [MMSLT Region Ablation (4K Training)](artifacts/mmslt-region-ablation-4k.html) | Blacks out each body region (MediaPipe Holistic landmarks) at test time and re-runs generation with the same checkpoint. The delta shows how much output quality depends on each region. Trained on a 4,000-sentence How2Sign slice; evaluated on 300 test sentences. |
| [Grounding or Guessing](artifacts/grounding-or-guessing.html) | Region-masking reliability of Qwen2.5-VL-3B-Instruct before and after LoRA fine-tuning on 4,000 How2Sign clips. Finding: fine-tuning did not teach the model to look; it made it guess more confidently. |
| [CLIP vs SignCLIP](artifacts/clip-vs-signclip.html) | Cross-check of two zero-shot vision-language scorers on which body region a cue word should ground to. Agreement is 13.6% vs. 13.2% expected by chance (+0.4pp), so neither scorer works as an "independent" reference for the other. |
| [Grounding Example Viewer (4K Training)](artifacts/grounding-viewer-4k.html) | Browse individual examples behind the aggregate numbers. |

## Setup (How2Sign reports)

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

- **How2Sign:** released under [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/). The reports include ground-truth sentences and downsampled frame thumbnails from the How2Sign test set (embedded in `artifacts/ptc/` and the example viewer) for non-commercial research illustration. Full videos are not redistributed.
- **WLASL:** used only for initial probing under its own terms of use (C-UDA). No WLASL data is included in this repository.
- **NIKL Korean Sign Language Corpus 2023, 2024:** used with approval from the National Institute of Korean Language for AI training and presentation at academic conferences and in publications, including this project page and demo. No corpus data is included in this repository.

## Citation / Contact

<!-- Add paper title, authors, and contact once public -->
