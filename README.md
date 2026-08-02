# Reproduction artifact — Budget-Matched Analysis of Compact Cross-Encoder Reranking in Hybrid Retrieval

Companion code and cached results for the IEEE Access article by Ibrahim Mohd
Jamadi and Syahid Anuar.

The article evaluates compact cross-encoder reranking across eight BEIR
collections and twelve systems under one protocol, holding the cross-encoder
*budget* fixed rather than the retained depth. This repository contains the
notebook that produced every reported number.

---

## What is here

| File | Contents |
|---|---|
| `HyR_MiniLM_Paper_Reproduction.ipynb` | Consolidated notebook, all outputs preserved as executed |
| `CITATION.cff` | Citation metadata |
| `LICENSE` | MIT |

Because every cell's output is stored in the notebook, each reported number can
be read directly from this repository without executing anything.

The notebook is organized in three parts:

- **Part I — Core experiments.** BM25 retrieval, E5 candidate selection,
  cross-encoder scoring, fusion, the component ablation, the peer benchmark,
  and the oracle and routing analyses.
- **Part II — Expansion analyses.** Gain-variance correlations, the
  corpus-size crossover fit, and the accuracy–latency frontier figure.
- **Part III — Recomputations.** The null-corrected oracle, budget-constrained
  leave-one-dataset-out selection, leave-one-signal-out attribution, and the
  judgement-coverage check.

A table at the top of the notebook maps every manuscript table and figure to
the cell that produced it.

## Scope of this artifact

This is **result reconstruction**, not full end-to-end reproduction. The
notebook regenerates every reported number from cached component scores.
Reproducing from scratch additionally requires re-running BM25 indexing, E5
document encoding (several hours and roughly 8 GB of FP16 embeddings), and
cross-encoder scoring on comparable hardware.

Datasets and pretrained checkpoints are obtained from their original providers
and are not redistributed here.

## Two known gaps

Reported openly rather than left for a reader to discover.

**1. Three tables cannot be regenerated from this notebook.** Manuscript
Tables 6, 7 and 23 derive from `Table_30_Budget_Matched_Comparison`,
`Table_31_Budget_Matched_Latency` and `Table_32_GTE_FullCorpus_Latency`. Part II
loads these from disk; the session that generated them was not saved. The
values as used are visible in the manuscript and in the Part II cell outputs
stored in the notebook.

**2. Five reranker latencies differ between notebook and manuscript.** Part I
§31 prints 51.279, 58.792, 80.188, 115.997 and 83.523 ms; manuscript Table 12
reports 51.6, 59.1, 80.2, 115.8 and 83.4. These came from separate runs of the
same benchmark. The differences are under 1% and affect no conclusion.

## Superseded results, retained deliberately

Two results are kept under a warning rather than deleted, so the correction
history stays visible:

- **Part I §34** reported a null-corrected headroom of 0.0804. The correction
  subtracted an oracle scored under permuted labels from a baseline scored
  under true labels — quantities not on a common scale, so the correction never
  fired. Superseded by **Part III §1.1**, which computes **0.0791** with both
  terms under the same labels.
- **Part I §22**, the end-to-end warm-query profile, was superseded by a later
  re-run at 128.10 ms per query, which is the figure the manuscript uses.

## Running it

Built for Google Colab with a GPU runtime. Paths currently point at
`/content/drive/MyDrive/HyR_MiniLM_BEIR_v2`; change `ROOT` in the setup cell to
run elsewhere.

Key settings, all fixed in the notebook: seed 42, BM25 `k1=1.5` `b=0.75`,
input length 512 for every encoder, FP16 cross-encoders, batch size 128 for all
latency measurement, `pytrec_eval` with linear gain, deterministic
document-identifier tie-breaking.

## Citing

Please cite the article, and the archived release if you use the code:

```bibtex
@article{jamadi2026budget,
  author  = {Mohd Jamadi, Ibrahim and Anuar, Syahid},
  title   = {Budget-Matched Analysis of Compact Cross-Encoder Reranking
             in Hybrid Retrieval},
  journal = {IEEE Access},
  year    = {2026}
}
```

## Licence

Code is released under the MIT Licence (see `LICENSE`). The cached CSV tables
and derived outputs are released under CC BY 4.0. BEIR collections and
pretrained model checkpoints remain under their own licences and are not
redistributed here.
