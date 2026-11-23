# Glyph tests

```bash
pip install -e ".[dev]"
pytest
```

`pyproject.toml` configures discovery: everything under `tests/` named `test_*.py`
or numbered like `test1_config.py`, with the repository root on the import path
so tests can import `examples/`. Run one file with `pytest tests/test_sae_selection.py`
and coverage with `pytest --cov=glyph --cov-report=html`.

## Optional tests

These skip unless their dependency or setting is present.

| Tests | Enable with |
| --- | --- |
| `test_confounder_adjustment.py`, part of `test_literature_harness.py` | `pip install -e ".[confounders]"` (xgboost) |
| `test_hf_embeddings.py` | `pip install -e ".[hf]"`; the real DINOv3 workflow also needs approved checkpoint access and `GLYPH_DINOV3_REAL=1` |
| `test_html_browser.py` | `pip install -e ".[browser-tests]"`, a Playwright Chromium and `GLYPH_BROWSER_TESTS=1` (optionally `GLYPH_CHROMIUM_EXECUTABLE`) |
| `test_labs_hf.py` | `GLYPH_HF_INTEGRATION=1` (downloads the public labs models) |
| `test_pretrained_reader_hf.py` | `GLYPH_READER_HF_INTEGRATION=1`; its CT case also needs `GLYPH_PUBLIC_CT_CASE` |
| `test_ct_parity.py` | `GLYPH_CT_PARITY_CASE`, a local case JSON (see the file docstring) |
| `test3_data.py`, `test4_embedding_extraction.py` | The pneumonia dataset at `/dataNAS/people/rholland/pneumonia_data`; test4 also downloads ResNet18 weights |

## Not pytest tests

- `chexpert1_test.py`, `chexpert2_test.py`, `feature1_test.py`, `feature2_test.py`,
  `test_autointerp.py`: integration scripts for private pneumonia/CheXpert data.
  Run with `python tests/<file>.py`.
- `check_labs_cache.py`: private lab-cache parity check.
- `test_dataset/download.py`: builds a local PneumoniaMNIST `metadata.csv` (needs `medmnist`).
- `reference/`: frozen research implementation that `test_confounder_adjustment.py` compares against.
