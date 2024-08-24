# Doshare-LLM-summarization

# PDF Summarization using Transformers

This repository provides Python scripts for extracting and summarizing text from PDF files using transformer-based models. The repository features two models: **DistilBART-cnn** and **BART-large-cnn**, both fine-tuned on the CNN/DailyMail dataset for summarization tasks.

## Table of Contents

- [Installation](#installation)
- [Usage](#usage)
  - [Script 1: DistilBART-cnn](#script-1-distilbart-cnn)
  - [Script 2: BART-large-cnn](#script-2-bart-large-cnn)
- [Files](#files)
- [Models Used](#models-used)
- [License](#license)

## Installation

Before running the scripts, install the required Python packages using pip:

``bash
pip install PyPDF2 transformers

The repository includes two scripts:

Script 1: DistilBART-cnn: This script extracts text from the first few pages of a PDF and summarizes it using the DistilBART-cnn model. It is ideal for quick summarization tasks where computational resources are limited.

Script 2: BART-large-cnn: This script automatically identifies an uploaded PDF file in a Colab environment, extracts and preprocesses the text, and generates a summary using the BART-large-cnn model. It is suitable for more detailed summarization tasks.

script1_distilbart.py: Script using DistilBART-cnn for summarization.

script2_bart_large.py: Script using BART-large-cnn for summarization in a Colab environment.

DistilBART-cnn: A smaller, faster version of the BART model, fine-tuned for summarization tasks on the CNN/DailyMail dataset.

BART-large-cnn: A larger BART model, also fine-tuned on the CNN/DailyMail dataset, providing more detailed and accurate summaries.

