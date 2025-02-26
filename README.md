# Fine-Tuning DistilBERT for Political Party Classification

This repository contains a Python notebook that fine-tunes a [DistilBERT](https://huggingface.co/distilbert/distilbert-base-uncased) model to classify political text segments into **Democrat** or **Republican**. For an in-depth explanation of the project’s motivation and methodology, please refer to the accompanying [overview.pdf](overview.pdf).

---

## Table of Contents
1. [Overview](#overview)  
2. [Dataset and Preprocessing](#dataset-and-preprocessing)  
3. [Model Architecture](#model-architecture)  
4. [Usage](#usage)  
5. [Results](#results)  
6. [Conclusion](#conclusion)  
7. [References](#references)  

---

## Overview

The purpose of this project is to determine whether a given text segment aligns more closely with the **Democratic** or **Republican** party platform. By analyzing party platform statements from 1948 to 2020, we sought to:

- **Demonstrate** how fine-tuning a smaller transformer model can yield improved classification on domain-specific text.
- **Explore** the challenges of political sentiment detection, including detecting subtle language cues and potential model bias.
- **Provide** a foundation for further research in detecting political leanings or bias in modern discourse.

For additional details, including the historical context of the dataset and deeper discussion of the approach, see [overview.pdf](overview.pdf).

---

## Dataset and Preprocessing

1. **Data Source**  
   - **Comparative Agendas Project**: Political party platform statements labeled “Democrat” or “Republican,” covering 1948–2020.  
   - **Manual Curation**: Supplemental test statements from news articles, social media posts by politicians, official 2024 DNC/RNC platforms, and other sources not in the original dataset.

2. **Cleaning & Transformation**  
   - Removed unnecessary features beyond text and party labels.  
   - Tokenized statements using Hugging Face’s `DistilBertTokenizer`.  
   - Partitioned data into training and validation sets.

---

## Model Architecture

- **Pretrained Base**: [DistilBERT](https://huggingface.co/distilbert/distilbert-base-uncased) (~67M parameters), noted for its efficiency relative to larger BERT models.  
- **Fine-Tuning**:  
  - Trained on our labeled dataset of political statements.  
  - Used cross-entropy loss with the AdamW optimizer.  
  - Required approximately 5 hours of training on a 2.3GHz 8-Core Intel i9 with a dataset containing ~5 million characters.

---

## Usage

To adapt this code, open the Python notebook in this repository and modify the cells as needed for your environment or data. You can adjust hyperparameters (epochs, learning rate, batch size, etc.) within the notebook.

---

## Results

1. **Model Comparison**  
   - **Non-Fine-Tuned DistilBERT**: Produced neutral or skewed predictions without strong alignment to either political party.  
   - **Fine-Tuned DistilBERT**: Displayed a moderate increase in accuracy and ROC AUC (from ~0.43 to ~0.60).

2. **Performance Highlights**  
   - **ROC Curve**: Demonstrates that the fine-tuned model outperforms random guessing but remains below the ideal threshold for robust deployment.  
   - **Confidence Distributions**: The fine-tuned model is more polarized in predictions than the base model, although it shows less certainty for some Republican-oriented text segments.

---

## Conclusion

This project illustrates both the promise and limitations of using a fine-tuned transformer model to classify political statements. While our model’s improved AUC (from ~0.43 to ~0.60) demonstrates that **fine-tuning can indeed boost performance**, it still falls short of deployment-ready accuracy. Key observations and future directions:

- **Expanded Training Data**: Leveraging a larger, more diverse dataset (including ambiguous or less overtly partisan statements) could help the model generalize beyond clear-cut statements.  
- **Hardware & Architecture**: Training on more powerful hardware or using a higher-parameter architecture (e.g., the full BERT or RoBERTa) may significantly improve results, albeit at higher computational cost.  
- **Bias & Fairness**: Political text often contains subtle framing. Additional steps, such as fairness metrics or multi-genre training, could mitigate potential biases.  
- **Retrieval-Based Systems**: Instead of strictly classifying party alignment, a retrieval-based approach could provide context (e.g., related documents or quotes) to enhance user understanding and reduce misclassification impact.

For a more thorough discussion of these points and the underlying motivations, be sure to consult the [overview.pdf](overview.pdf) located in this repository.

---

## References

1. Jones, Bryan. “United States.” *Comparative Agendas*,  
   [www.comparativeagendas.net/us](https://www.comparativeagendas.net/us). Accessed 20 Dec. 2024.  
2. “Google-Bert/Bert-Base-Uncased · Hugging Face.”  
   [huggingface.co/google-bert/bert-base-uncased](https://huggingface.co/google-bert/bert-base-uncased). Accessed 20 Dec. 2024.  
3. “Distilbert/Distilbert-Base-Uncased · Hugging Face.”  
   [huggingface.co/distilbert/distilbert-base-uncased](https://huggingface.co/distilbert/distilbert-base-uncased). Accessed 20 Dec. 2024.  
4. “Legacy-Datasets/Wikipedia · Datasets at Hugging Face.”  
   [huggingface.co/datasets/legacy-datasets/wikipedia](https://huggingface.co/datasets/legacy-datasets/wikipedia). Accessed 20 Dec. 2024.  
5. Bookcorpus. “Bookcorpus/Bookcorpus · Datasets at Hugging Face.”  
   [huggingface.co/datasets/bookcorpus/bookcorpus](https://huggingface.co/datasets/bookcorpus/bookcorpus). Accessed 20 Dec. 2024.  
6. “MacBook Pro (16-Inch Late 2019) Benchmarks.” *Geekbench Browser*,  
   [browser.geekbench.com](https://browser.geekbench.com/macs/macbook-pro-16-inch-late-2019-intel-core-i9-9880h-2-3-ghz-8-cores). Accessed 20 Dec. 2024.  

---

*Thank you for exploring this project! Please open an issue or submit a pull request if you have suggestions or would like to contribute.*
