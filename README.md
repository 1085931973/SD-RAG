# SD-RAG

SD-RAG is a domain-specific retrieval-augmented generation framework for question answering over power-industry standard documents.

The project is designed around a routed RAG workflow: a user question is first routed to the most relevant standard-document domains, then relevant passages are retrieved from the selected document collections, reranked, and used to generate a grounded answer.

This initial repository release contains only documentation and placeholder folders. Source code, datasets, indexes, model checkpoints, and experiment outputs are not included in this version.

## Introduction

Power-industry standards contain dense technical requirements across equipment operation, maintenance, safety, environmental protection, metering, construction, information technology, and material testing. A single flat retrieval index can retrieve noisy passages when questions involve specialized terminology or cross-domain standards.

SD-RAG addresses this by introducing a domain-routing stage before retrieval. The intended pipeline contains four main stages:

1. Route the question to the top-2 relevant power-standard domains.
2. Retrieve top-k candidate passages from the selected domain collections.
3. Rerank the retrieved passages with a domain-aware reranker.
4. Generate the final answer from the highest-quality supporting evidence.

## Dataset Construction

The dataset construction process follows a standard-document-centered workflow.

1. Collect power-industry standard documents from multiple technical domains.
2. Organize documents by domain categories, including:
   - operation, maintenance, testing, and servicing of power equipment and systems;
   - environmental protection, energy conservation, and comprehensive resource utilization;
   - verification of measuring instruments;
   - power engineering survey, planning, design, construction, commissioning, and acceptance;
   - labor protection and production safety;
   - computer applications and information technology;
   - testing, measurement, supervision, quality evaluation, and technical conditions for equipment and materials.
3. Convert source documents into Markdown or plain-text representations.
4. Split long documents into retrievable chunks while preserving document titles, section hierarchy, and domain metadata.
5. Build QA samples with fields such as `instruction`, `output`, `chunk`, `classification`, and `route`.
6. Add top-2 route labels for each question so that routing quality can be evaluated before retrieval and answer generation.

The dataset itself is not included in this repository. Future releases may provide metadata, construction scripts, and sanitized examples when redistribution conditions are clear.

## Environment Setup

The full implementation is not released in this initial version, but the planned development environment is:

```bash
conda create -n zjenv python=3.10
conda activate zjenv
```

Main dependency categories:

- PyTorch for model inference and training;
- Transformers and related model-loading utilities;
- FAISS for dense-vector indexing and nearest-neighbor retrieval;
- sentence-transformers or other embedding model interfaces;
- reranking model dependencies;
- requests for model API calls;
- tqdm, numpy, pandas, and scikit-learn for data processing and evaluation;
- matplotlib for visualization;
- optional RAG evaluation tools for answer-quality analysis.

Exact installation commands will be added when the implementation code is released.

## Demo

The demo is intended to show the user-facing SD-RAG workflow:

1. The user submits a power-domain question.
2. The interface displays the routing stage and returns the top-2 selected domains.
3. The retrieval stage collects relevant candidate passages.
4. The reranking stage refines the evidence order.
5. The final answer is streamed to the interface.

The current repository only documents the demo behavior. Demo source code and backend logic are not included in this initial release.

## Repository Structure

```text
SD-RAG/
├── README.md
├── dataset/
├── dataset_preparation/
├── demo/
└── docs/
```

- `dataset/`: placeholder for future dataset release notes or metadata.
- `dataset_preparation/`: placeholder for future data-construction scripts.
- `demo/`: placeholder for future demo assets and instructions.
- `docs/`: placeholder for additional documentation.

## Future Updates

Planned updates include:

- dataset construction scripts;
- document chunking and metadata-generation utilities;
- route-aware retrieval pipeline;
- reranking and answer-generation modules;
- demo implementation;
- evaluation scripts and benchmark reports;
- processed dataset metadata or sanitized examples.

## Acknowledgement

The repository organization is inspired by the clean initial-release style of [Henry-Zhao-sz/wind-farm-recon](https://github.com/Henry-Zhao-sz/wind-farm-recon).
