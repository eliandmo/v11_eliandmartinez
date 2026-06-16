# Reproducibility Guide

This document explains how to reproduce the notebook results and how to interpret possible differences across environments.

## Recommended Execution Environment

The notebook was designed for Google Colab. A GPU runtime is recommended for faster embedding generation, but CPU execution is possible.

Recommended runtime:

```text
Google Colab
Python 3.10+
GPU runtime when available
```

## Installation

Install the required packages with:

```bash
pip install -r environment/requirements.txt
python -m spacy download en_core_web_sm
```

In Google Colab, the notebook includes installation cells.

## Input Files

Before running the notebook, make sure the following files exist:

```text
data/scopus_final_with_references.csv
data/thesaurus_bibliometrix_elian.csv
```

The notebook can also download files from Google Drive if configured with the corresponding file IDs.

## Random Seed

The notebook sets:

```python
SEED = 42
```

It also fixes several environment variables to reduce run-to-run variability. Even so, exact reproducibility cannot be fully guaranteed across hardware and library versions. UMAP, HDBSCAN, transformer embeddings, and GPU computations may produce small numerical differences.

## OpenAI-Assisted Labeling

The OpenAI labeling step requires:

```text
OPENAI_API_KEY
```

This key is private and must not be committed to GitHub.

In Google Colab, store it under Secrets as:

```text
OPENAI_API_KEY
```

If the key is not available, the notebook still exports:

- prompt template,
- prompt examples,
- representative abstracts for labeling.

This allows the labeling procedure to be inspected even when API calls are not executed.

## Optional Llama 3.1 Alternative

The repository includes an optional notebook for local or API-free topic labeling experiments:

```text
notebooks/bertopic_thesis_reanalysis_llama31_local_optional.ipynb
```

This notebook is included only as an alternative for reviewers who cannot run OpenAI-assisted labeling. It should not be treated as the canonical notebook for the thesis results. Local Llama outputs may differ from the OpenAI-assisted labels because they depend on the selected model, quantization, GPU memory, runtime environment, and prompt behavior.

## Expected Core Outputs

The selected model configuration should be checked against:

```text
outputs/grid/embedding_hyperparameter_grid_results.csv
outputs/tables/selected_model_diagnostics.csv
```

The final topic labels should be checked against:

```text
outputs/tables/selected_topic_inventory_with_final_labels.csv
```

The figures used in the thesis are stored in both PNG and PDF formats:

```text
outputs/figures/
```

## Notes on CPU vs GPU Differences

Running the notebook on CPU and GPU may produce slight differences in the number of topics or outliers. This can occur because floating-point operations, nearest-neighbor search, dimensionality reduction, and clustering can behave slightly differently across computational backends.

For thesis reporting, use one fixed execution environment and report the results obtained from that environment.
