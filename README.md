# Fine-Tuning DistilBERT for Political Party Classification

This repository contains a Python notebook that fine-tunes a [DistilBERT](https://huggingface.co/distilbert/distilbert-base-uncased) model to classify political text segments into **Democrat** or **Republican**. The approach, dataset, and results are outlined below, along with instructions for setup and usage.

---

## Table of Contents
1. [Overview](#overview)  
2. [Dataset and Preprocessing](#dataset-and-preprocessing)  
3. [Model Architecture](#model-architecture)  
4. [Usage](#usage)  
5. [Results](#results)  
6. [Conclusions](#conclusions)  
7. [References](#references)  

---

## Overview

This project demonstrates how to fine-tune a pretrained language model on a specific text classification task—political sentiment analysis—using statements labeled as either “Democrat” or “Republican.” The goals include:

- **Exploring** how a smaller transformer model (DistilBERT) performs on nuanced text classification.  
- **Evaluating** the effectiveness of fine-tuning a base model on political statements spanning multiple years.  
- **Identifying** shortcomings of the model and discussing possible improvements.  

**Motivation:**  
Classifying text segments by political party can help researchers, political analysts, and the general public better understand bias, alignment, or stance in political discourse. This can be extended to detecting leaning or bias in various news and social media sources.

---

## Dataset and Preprocessing

### Data Source
- **Platform Statements**: Training data primarily comes from the [Comparative Agendas Project](https://www.comparativeagendas.net/), which aggregates party platforms (Democrat and Republican) from 1948 to 2020. Each segment is labeled by party affiliation.  
- **Additional Variables**: Original datasets included multiple variables; only statement text and party label were retained in the final training corpus.

### Data Engineering
- **Cleaning**: Removed extraneous formatting, metadata, and unused columns.  
- **Splitting**: Reserved a subset of data for validation.  
- **Tokenization**: Utilized Hugging Face’s `DistilBertTokenizer` to encode text for input to the model.  

---

## Model Architecture

### Base Model
- **DistilBERT**: A lightweight variant of [BERT](https://huggingface.co/google-bert/bert-base-uncased), with ~67 million parameters. Pretrained on large text corpora such as Wikipedia and BookCorpus.  
- **Why DistilBERT?**: Offers significantly reduced computational cost and memory footprint while retaining strong language comprehension capabilities.

### Fine-Tuning
- **Hardware**: Training was performed on a 2.3GHz 8-Core Intel i9 (2019 MacBook Pro), requiring ~5 hours on a ~5 million character training set.  
- **Loss & Optimizer**: Standard cross-entropy with AdamW.  
- **Hyperparameters**:  
  - Epochs: ~3–5 (adjust as needed)  
  - Batch size: 16–32 (memory dependent)  
  - Learning rate: 2e-5 (tuned experimentally)  

---

## Usage

1. **Clone This Repository**  
   ```bash
   git clone https://github.com/YourUsername/Political-Sentiment-Classification.git
   cd Political-Sentiment-Classification
