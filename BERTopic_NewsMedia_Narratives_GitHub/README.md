# BERTopic Analysis of Narrative Structures in News Media Scholarship

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1nBhS0jCXixKShqDUBELZF9kBDaEQMYs0?usp=sharing)

This repository contains the reproducible notebook, input data, and selected outputs used for the BERTopic-based analysis of scientific publications related to storytelling, narratives, and news media.

The project supports the thesis workflow by documenting:

- corpus construction from Scopus records,
- abstract-level BERTopic modeling,
- embedding and hyperparameter comparison,
- topic diagnostics and model selection,
- OpenAI-assisted topic labeling,
- outlier review,
- export of figures and tables in reproducible formats.

## Repository Structure

```text
BERTopic_NewsMedia_Narratives_GitHub/
|
|-- data/
|   |-- scopus_final_with_references.csv
|   `-- thesaurus_bibliometrix_elian.csv
|
|-- notebooks/
|   |-- bertopic_thesis_reanalysis_openai.ipynb
|   `-- bertopic_thesis_reanalysis_llama31_local_optional.ipynb
|
|-- outputs/
|   |-- figures/
|   |-- grid/
|   |-- labeling_evidence/
|   |-- outliers/
|   `-- tables/
|
|-- environment/
|   `-- requirements.txt
|
|-- DATA_DICTIONARY.md
|-- REPRODUCIBILITY.md
|-- DATA_NOTICE.md
|-- GITHUB_UPLOAD_STEPS.md
`-- README.md
```

## Main Notebook

The canonical notebook for thesis verification is the Google Colab notebook:

```text
https://colab.research.google.com/drive/1nBhS0jCXixKShqDUBELZF9kBDaEQMYs0?usp=sharing
```

A repository copy is included as:

```text
notebooks/bertopic_thesis_reanalysis_openai.ipynb
```

It performs the complete abstract-level analysis:

1. Loads the Scopus corpus and thesaurus.
2. Filters records with usable abstracts.
3. Generates sentence embeddings.
4. Compares BERTopic configurations.
5. Selects the best model based on the defined metrics.
6. Exports topic inventories, diagnostics, and figures.
7. Documents OpenAI-assisted topic labeling.
8. Reviews outlier documents.

The same notebook can be opened directly in Google Colab through the badge above.

## Optional Llama 3.1 Notebook

An optional notebook is included for API-free topic labeling experiments:

```text
notebooks/bertopic_thesis_reanalysis_llama31_local_optional.ipynb
```

This notebook is not the primary thesis notebook. It is included only as a reproducibility alternative for reviewers who do not have access to an OpenAI API key. Because local LLM execution depends on available GPU memory, quantization, runtime configuration, and model behavior, its labels may differ from the OpenAI-assisted labels reported in the main notebook.

## Data

The analysis uses two input files:

```text
data/scopus_final_with_references.csv
data/thesaurus_bibliometrix_elian.csv
```

The corpus file contains the final Scopus records used in the thesis. The thesaurus file contains term normalization rules used for bibliometric and keyword-related cleaning.

## OpenAI Labeling Note

The OpenAI-assisted labeling stage requires an API key. The key is not included in this repository.

If running in Google Colab, add the key through:

```python
from google.colab import userdata
userdata.get("OPENAI_API_KEY")
```

The repository includes the prompt template and representative abstracts used for labeling, so the labeling procedure can be reviewed even without executing API calls:

```text
outputs/labeling_evidence/openai_prompt_template.txt
outputs/labeling_evidence/openai_prompt_examples.csv
outputs/labeling_evidence/representative_abstracts_for_labeling.csv
```

## Key Outputs

Selected outputs are included so the thesis results can be checked without rerunning the entire notebook.

### Model Selection

```text
outputs/grid/embedding_hyperparameter_grid_results.csv
outputs/tables/selected_model_diagnostics.csv
```

### Topic Results

```text
outputs/tables/selected_topic_inventory_with_final_labels.csv
outputs/tables/selected_topic_info_raw.csv
outputs/tables/selected_document_topic_assignments.csv
```

### Figures

```text
outputs/figures/embedding_hyperparameter_grid_summary.png
outputs/figures/embedding_hyperparameter_grid_summary.pdf
outputs/figures/selected_topic_prevalence.png
outputs/figures/selected_topic_prevalence.pdf
outputs/figures/selected_representative_ctfidf_terms.png
outputs/figures/selected_representative_ctfidf_terms.pdf
outputs/figures/selected_bertopic_umap_topic_map.png
outputs/figures/selected_bertopic_umap_topic_map.pdf
```

### Outlier Review

The repository includes both the outlier document list and the supporting review files:

```text
outputs/outliers/outlier_documents_for_review.csv
outputs/outliers/outlier_documents_exhaustive_review_enriched.csv
outputs/outliers/outlier_documents_review_enriched.csv
outputs/outliers/outlier_review_summary_metrics.csv
outputs/outliers/outlier_review_report.md
outputs/outliers/outlier_year_distribution.csv
outputs/outliers/outlier_top_sources.csv
outputs/outliers/outlier_keyword_category_counts.csv
outputs/outliers/outlier_closest_topic_lexical_summary.csv
outputs/outliers/outlier_nmf_thematic_subgroups.csv
outputs/outliers/outlier_recommended_actions.csv
outputs/outliers/outlier_vs_assigned_comparison.csv
```

## Reproducibility

The notebook fixes the random seed where possible:

```python
SEED = 42
```

However, small differences may still occur across CPU/GPU environments, operating systems, or library versions, especially in UMAP, HDBSCAN, and transformer embedding generation.

For details, see:

```text
REPRODUCIBILITY.md
```

## Suggested Citation

If this repository is referenced in academic review, cite it as supporting material for:

```text
Martinez, E. Thesis repository for BERTopic-based analysis of narrative structures in news media scholarship.
```

## Author

Elian Martinez  
Universidad del Norte

