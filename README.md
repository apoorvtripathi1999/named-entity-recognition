# Medical Named Entity Recognition (NER) with Enhanced RAG Systems

A research project focused on improving Named Entity Recognition in medical text using advanced Retrieval Augmented Generation (RAG) techniques, enhanced prompting strategies, and multi-database support.

## Overview

This project addresses the challenge of extracting meaningful entities from unstructured clinical data, which comprises over 80% of all clinical information. The system builds upon existing DIRAG (Dictionary Infused Retrieval Augmented Generation) and KATE (KNN-Augmented in-context Example selection) frameworks to provide more robust and efficient medical NER capabilities.

## Key Features

### Core Capabilities
- **Zero-Shot Classification**: Entity recognition without training examples
- **One-Shot Classification**: Entity recognition with contextual examples using KATE
- **Multi-Format Support**: Handles tabular data, paragraphs, and large medical documents
- **Context-Aware Processing**: Addresses the challenge of medical terms with multiple contextual meanings

### Novel Enhancements

#### 1. Advanced Prompting Techniques
- Integration of **Chain of Thought** prompting with TANL
- **Meta-prompting** techniques for improved entity extraction
- Enhanced TANL/DICE prompt formatting for better LLM comprehension

#### 2. Intelligent Caching System
- Reduces computational costs for RAG-based lookups
- Stores previously retrieved context for reuse
- Significantly improves system efficiency and response time

#### 3. Multi-Database Entity Classification
- **Dynamic database selection** based on entity type:
  - NCBI Gene database for gene variants
  - UMLS for general medical terminology
  - Specialized databases for drugs, chemicals, pathways
- Pre-classification of entity types before context retrieval
- Expanded application scope beyond the original UMLS-only approach

## System Architecture

### Pipeline Overview

```
Input Text
    ↓
Potential Entity Identification
    ↓
    ├─→ One-Shot (KATE) ──→ BioClinicalBERT/RoBERTa Embeddings
    │                        ↓
    │                    KNN Matching
    │                        ↓
    │                    Contextual Examples
    │
    └─→ Zero-Shot (DIRAG) ─→ Entity Type Classification
                              ↓
                          Database Selection (NCBI/UMLS/etc.)
                              ↓
                          Context Retrieval (with Caching)
    ↓
Final Entity Recognition TANL/DICE Format (Enhanced with CoT/Meta-prompting)
```

## Technical Components

### Models Used
- **BioClinicalBERT**: For generating semantic embeddings
- **BioClinicalRoBERTa**: Alternative embedding model
- **GPT/BERT/Llama**: LLM backbone for entity recognition

### Databases
- **UMLS** (Unified Medical Language System): General medical terminology
- **NCBI Gene**: Gene variants and genetic information
- **PubMed**: Medical literature context
- **Domain-specific databases**: Drugs, chemicals, pathways

### Frameworks
- **TANL** (Translation between Augmented Natural Languages): Prompt formatting
- **DICE** (Dimensional and Contextual Evaluation): Contextual prompt generation
- **KATE** (KNN-Augmented in-context Example selection): Example-based learning
- **DIRAG** (Dictionary Infused Retrieval Augmented Generation): Zero-shot context retrieval

## Research Challenges Addressed

1. **Multiple Text Formats**: Handling diverse medical document structures
2. **Contextual Ambiguity**: Resolving multiple meanings of medical terms
3. **Application Diversity**: Supporting various NER tasks (gene mutations, symptoms, diseases, drug effects)
4. **Resource Efficiency**: Reducing computational costs through caching
5. **Scalability**: Enabling multi-database support for broader applications

## Dataset

The project uses medical datasets including:
- `data/data_NCBI_Test.csv`: NCBI test dataset
- `data-words/train.tsv`: Training data

## Getting Started

### Prerequisites
```bash
# Python dependencies (adjust as needed)
- transformers
- torch
- pandas
- scikit-learn
- numpy
```

### Installation
```bash
# Clone the repository
git clone https://github.com/apoorvtripathi1999/named-entity-recognition.git
cd named-entity-recognition

# Install dependencies
pip install -r requirements.txt
```

### Usage
Open and run the Jupyter notebook:
```bash
jupyter notebook basemodel.ipynb
```

## Project Structure

```
NLP/
├── basemodel.ipynb          # Main research notebook
├── data/                    # Dataset directory
│   └── data_NCBI_Test.csv  # NCBI test data
├── data-words/             # Training data
│   └── train.tsv          # Training dataset
└── README.md              # This file
```

## Improvements Over Baseline

| Feature | Baseline | This Study |
|---------|----------|------------|
| Prompting | TANL/DICE only | Enhanced with CoT and meta-prompting |
| Database Support | UMLS only | Multi-database (NCBI, UMLS, etc.) |
| Resource Efficiency | No caching | Intelligent caching system |
| Entity Type Coverage | Limited | Gene variants, drugs, chemicals, pathways |
| Application Scope | Narrow | Broad, multi-domain support |

<!-- ## Future Work

- Expand database integrations
- Optimize caching strategies
- Benchmark performance across diverse medical NER tasks
- Explore additional prompting techniques
- Develop real-time inference capabilities -->

## References

- Muralikrishna (2025). Clinical data analysis and unstructured data challenges
- Masoud Monajatipoor (2023). RAG-based systems for Named Entity Detection

## Contributors

Apoorv Tripathi ([@apoorvtripathi1999](https://github.com/apoorvtripathi1999))


<!-- ## Citation

If you use this work in your research, please cite:
```bibtex
[Add citation format when available]
```

--- -->

**Note**: This is an active research project. The methodology and implementation are subject to ongoing refinement and improvement.
