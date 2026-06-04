# microRNA-GPT

GPT-style biological sequence modeling pipeline for **pre-miRNA sequence generation and analysis**.

This project explores how language-modeling techniques can be applied to biological sequence data. It includes data preprocessing, sequence filtering, tokenizer training, GPT-style pretraining, human-specific fine-tuning, generation, and biological feature extraction.

## Motivation

Biological sequences can be represented as token sequences, making them a natural fit for language-modeling approaches. In this project, a GPT-style model is trained to learn structure in pre-miRNA sequences and generate biologically plausible candidates.

The project focuses on the complete modeling workflow:

```text
Raw miRNA Data
      ↓
Preprocessing + Filtering
      ↓
Tokenizer Training
      ↓
GPT-Style Pretraining
      ↓
Human-Specific Fine-Tuning
      ↓
Sequence Generation
      ↓
Feature Extraction + Evaluation
```

## Main Capabilities

- Data collection and preprocessing for microRNA datasets
- Configurable preprocessing through `preprocess_config.ini`
- Sequence filtering and biological feature extraction
- Custom tokenizer training for nucleotide sequences
- GPT-style model training on preprocessed sequence data
- Human-specific fine-tuning
- Sequence generation from trained models
- Post-generation feature extraction for biological analysis

## Repository Structure

```text
.
├── Data_source/                              # input/source data
├── Data_output/                              # processed outputs
├── preprocess.py                            # preprocessing pipeline
├── preprocess_config.ini                    # paths and preprocessing settings
├── utils.py                                 # helper functions
├── tokenization.ipynb                       # tokenizer training
├── Pretrained_mature_star_after_preprocess.ipynb
├── Human_fine_tune_star_mature.ipynb
├── preprocess_clusters.ipynb
├── Extract_features_only_nts.ipynb
└── README.md
```

## Workflow

### 1. Configure preprocessing

Edit `preprocess_config.ini` and set the input/output paths.

```ini
[input]
# path_to_raw_data = ...

[output]
# path_to_processed_data = ...
```

### 2. Run preprocessing

```bash
python preprocess.py
```

The preprocessing stage collects sequences, applies filtering logic, extracts biological features, and prepares the data for tokenizer training and model training.

### 3. Train tokenizer

Open and run:

```text
tokenization.ipynb
```

This notebook trains a tokenizer over the biological sequence corpus. Depending on the experiment, this can be adapted to character-level, k-mer, BPE, or other tokenization strategies.

### 4. Pretrain the model

Open and run:

```text
Pretrained_mature_star_after_preprocess.ipynb
```

This stage trains a GPT-style model on the preprocessed sequence corpus.

### 5. Fine-tune on human sequences

Open and run:

```text
Human_fine_tune_star_mature.ipynb
```

This stage adapts the pretrained model to human-specific data.

### 6. Generate and evaluate sequences

Use the fine-tuned model to generate candidate sequences, then extract features using:

```text
Extract_features_only_nts.ipynb
```

## Suggested Evaluation Section to Add

Add your final results here once you collect them:

| Experiment | Tokenization | Training Data | Evaluation Signal | Result |
|---|---|---|---|---|
| Pretraining | TODO | TODO | TODO | TODO |
| Human fine-tuning | TODO | TODO | TODO | TODO |
| Generation | TODO | TODO | TODO | TODO |

Good evaluation signals to include:

- sequence length distribution
- nucleotide composition
- GC content
- mature/star region validity
- similarity to known sequences
- duplicate rate
- biological feature distribution compared to real data

## Installation

```bash
conda create -n mirna-gpt python=3.10 -y
conda activate mirna-gpt

pip install pandas numpy scikit-learn matplotlib seaborn biopython
pip install torch transformers tokenizers datasets accelerate
```

## Usage

```bash
python preprocess.py
```

Notebook order:

```text
1. tokenization.ipynb
2. Pretrained_mature_star_after_preprocess.ipynb
3. preprocess_clusters.ipynb
4. Human_fine_tune_star_mature.ipynb
5. Extract_features_only_nts.ipynb
```

## Engineering Notes

This project treats biological sequence modeling as a language-modeling problem. The most important engineering choices are the tokenization strategy, data filtering, train/test split design, and biological evaluation after generation.

## Future Work

- Convert notebooks into CLI scripts
- Add experiment tracking with Weights & Biases or MLflow
- Add formal train/validation/test split reports
- Add generated-sequence examples
- Compare character-level, k-mer, and BPE tokenization
- Add model cards for trained checkpoints
