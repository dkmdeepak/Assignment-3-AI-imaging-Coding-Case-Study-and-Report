# Biomedical Image Pipeline — Stained Nuclei

raw image -> segmentation -> object measurements -> JSON record -> short text summary

All AI models run locally with Ollama. Every number in the final record is
computed in Python and put in directly — the AI model only picks a label
from a fixed list and writes the paragraph.

Educational use only. Not for real medical diagnosis.

## Files

- `biomedical_pipeline.ipynb` — the whole pipeline in one notebook (Tasks 1–4, plus an extra robustness check)
- `nuclei_dataset.zip` — 112 images + 4 damaged copies
- `figs/` — figures saved when the notebook runs
- `out/` — CSV/JSON results saved when the notebook runs

There is **no separate code package** — every function is defined directly
inside the notebook, in the cell for the task it belongs to. This means
there is nothing to import and nothing that can go "not found": just open
the notebook and run the cells top to bottom.

## Setup

```bash
pip install torch torchvision scikit-image matplotlib pandas pillow scipy
```

Put `nuclei_dataset.zip` in the same folder as the notebook (already done
here). The first code cell unzips it automatically if it is not already
unzipped — you do not need to unzip it by hand.

### Local AI models (optional but recommended)

```bash
ollama serve                     # in a separate terminal, leave it running
ollama pull llama3.2-vision      # used for Task 1 (image description)
ollama pull llava:7b             # backup model, used automatically if the above fails
ollama pull llama3.1:8b          # used for Task 2 and Task 4 (text-only steps)
```

If Ollama is not installed or not running, the notebook still runs from
start to end — it uses a simple built-in backup answer instead, and always
prints which one it used (`"ollama"` or `"offline-backup"`), so nothing is
hidden.

## Running

Open `biomedical_pipeline.ipynb` and run all cells, top to bottom. Figures
go into `figs/`, and CSV/JSON results go into `out/` — these are what the
report should use.
