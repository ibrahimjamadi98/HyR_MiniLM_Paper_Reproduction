# Reproduction artifact - Interaction-Budget-Matched Analysis of Compact Cross-Encoder Reranking in Hybrid Retrieval

Companion code and executed results for the manuscript **"Interaction-Budget-Matched Analysis of Compact Cross-Encoder Reranking in Hybrid Retrieval"**, prepared for submission to *IEEE Access*, by Ibrahim Mohd Jamadi, Syahid Anuar, Saad M. Ijad, and Mohamed Alkaoud.

The study evaluates compact hybrid retrieval across eight BEIR collections. Its primary comparison controls the number of query-document pairs processed by the cross-encoder and reports total online latency, memory, and offline storage separately. Under budget-constrained leave-one-dataset-out selection, the shallow hybrid configuration reranks 80.5 candidates per query versus 100 for standalone MiniLM-L4 and improves Macro-8 nDCG@10 from 0.4607 to 0.5136. In the measured environment, the complete hybrid pipeline has higher mean online latency: 98.83 ms versus 88.94 ms.

The conclusion is deliberately bounded: careful candidate selection and multi-signal fusion can improve compact reranking while using fewer cross-encoder interactions, but this does not imply equal total compute or universal superiority over stronger dense systems.

## Repository contents

| File | Contents |
| --- | --- |
| `HyR_MiniLM_Paper_Reproduction.ipynb` | Complete executed reproduction notebook with source code, narrative, tables, figures, and preserved outputs |
| `CITATION.cff` | Citation metadata for the software artifact and manuscript |
| `LICENSE` | MIT license for the repository code |

The notebook is organized into four parts:

1. **Core experimental workflow** - dataset loading, BM25S retrieval, E5 semantic selection, MiniLM reranking, score fusion, evaluation, statistical testing, candidate-depth analysis, peer systems, resource profiling, and routing experiments.
2. **Extended diagnostic analyses** - gain and variance analysis, the latency frontier, and exact-dense scalability analysis.
3. **Robustness and selection-separated analyses** - null-corrected oracle analysis, budget-constrained leave-one-dataset-out selection, leave-one-signal-out attribution, and judgement coverage.
4. **Extended validation and resource analysis** - matched-interaction component attribution, expanded warm-query profiling, query and document characteristics, resource accounting, and BM25 reconciliation.

## Reproducibility scope

The notebook retains the code used to obtain the BEIR collections, build BM25S indexes, encode E5 document representations, construct hybrid candidate pools, score query-document pairs, evaluate retrieval runs, perform statistical analyses, profile latency and resources, and export the study tables.

Saved outputs support inspection without rerunning the expensive stages. Generated indexes, embeddings, scores, and runs may be cached during execution, but these caches are acceleration artifacts rather than the source definition of the experiment. Dataset files and pretrained model checkpoints are obtained from their original providers and are not redistributed.

A matched budget in this work means a **matched cross-encoder interaction budget**. It does not mean equal total system computation, latency, memory, or storage.

## Running the notebook

The notebook was executed in Google Colab with an NVIDIA A100 GPU. Its default persistent path is:

```text
/content/drive/MyDrive/HyR_MiniLM_BEIR_v2
```

Change `ROOT` in the setup cell when running elsewhere. The recorded environment includes Python 3.13.15, PyTorch 2.11.0+cu128, Transformers 5.16.1, Sentence-Transformers 5.7.0, BEIR 2.2.0, BM25S 0.3.11, scikit-learn 1.6.1, SciPy 1.16.3, pandas 2.2.3, NumPy 2.1.3, and FlagEmbedding 1.4.2.

Key controlled settings include seed 42, BM25 `k1=1.5` and `b=0.75`, maximum sequence length 512, FP16 neural inference on GPU, BEIR-comparable evaluation through `pytrec_eval`, and deterministic document-identifier tie-breaking.

Absolute latency depends on hardware and software configuration. Reproducing the ranking results and reproducing the exact millisecond measurements are therefore separate goals.

## Archived release

The matching Zenodo release is **v1.1.0**:

- Version DOI: [10.5281/zenodo.22867583](https://doi.org/10.5281/zenodo.22867583)
- Concept DOI for all versions: [10.5281/zenodo.21755305](https://doi.org/10.5281/zenodo.21755305)

## Citation

Please cite the manuscript and the archived software release when using this artifact.

```bibtex
@article{jamadi2026interaction,
  author  = {Mohd Jamadi, Ibrahim and Anuar, Syahid and Ijad, Saad M. and Alkaoud, Mohamed},
  title   = {Interaction-Budget-Matched Analysis of Compact Cross-Encoder Reranking in Hybrid Retrieval},
  journal = {IEEE Access},
  year    = {2026}
}

@software{jamadi2026reproduction,
  author  = {Mohd Jamadi, Ibrahim and Anuar, Syahid and Ijad, Saad M. and Alkaoud, Mohamed},
  title   = {Reproduction artifact for "Interaction-Budget-Matched Analysis of Compact Cross-Encoder Reranking in Hybrid Retrieval"},
  version = {v1.1.0},
  year    = {2026},
  doi     = {10.5281/zenodo.22867583},
  url     = {https://doi.org/10.5281/zenodo.22867583}
}
```

## License

The repository code is released under the MIT License. BEIR collections and pretrained model checkpoints remain under their respective licenses.
