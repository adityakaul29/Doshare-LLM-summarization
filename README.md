# Doshare-LLM-summarization

PDF Summarization using Transformers
This repository contains Python scripts that extract and summarize text from PDF files using transformer-based models. The scripts leverage PyPDF2 for PDF text extraction and Hugging Face's transformers library for summarization. Two models are used:

DistilBART-cnn: A distilled version of the BART model fine-tuned on the CNN/DailyMail dataset.
BART-large-cnn: A larger BART model fine-tuned on the CNN/DailyMail dataset.
Table of Contents
Installation
Usage
Files
Models Used
License
Installation
To use the scripts, you'll need to install the necessary Python libraries. You can install them using pip:

bash
Copy code
pip install PyPDF2 transformers
Usage
Script 1: Using DistilBART-cnn
This script extracts text from the first few pages of a PDF and summarizes it using the DistilBART-cnn model.

python
Copy code
import PyPDF2
from transformers import pipeline

def extract_text_from_pdf(pdf_path, max_pages=3):
    with open(pdf_path, 'rb') as file:
        reader = PyPDF2.PdfReader(file)
        text = ""
        num_pages = min(len(reader.pages), max_pages)
        for page in range(num_pages):
            text += reader.pages[page].extract_text()
    return text

def summarize_text(text, max_length=100, min_length=30):
    summarizer = pipeline("summarization", model="sshleifer/distilbart-cnn-12-6")
    return summarizer(text, max_length=max_length, min_length=min_length, do_sample=False)[0]['summary_text']

if __name__ == "__main__":
    file_name = 'your-pdf-file.pdf'
    pdf_path = f'/content/{file_name}'
    
    text = extract_text_from_pdf(pdf_path, max_pages=3)
    summary = summarize_text(text, max_length=100, min_length=30)
    
    print("\nSummary:")
    print(summary)
Script 2: Using BART-large-cnn
This script automatically identifies the uploaded PDF in a Colab environment, extracts text, preprocesses it, and generates a summary using the BART-large-cnn model.

python
Copy code
import PyPDF2
from transformers import pipeline
import os

def get_uploaded_file():
    files = [f for f in os.listdir('/content') if f.endswith('.pdf')]
    return files[0] if files else None

def extract_text_from_pdf(pdf_name, max_pages=None):
    pdf_path = f'/content/{pdf_name}'
    text = ""
    with open(pdf_path, 'rb') as file:
        reader = PyPDF2.PdfReader(file)
        total_pages = len(reader.pages)
        num_pages = min(total_pages, max_pages) if max_pages else total_pages
        for page in range(num_pages):
            text += reader.pages[page].extract_text()
    return text

def preprocess_text(text):
    return " ".join(text.split())

def summarize_text(text, max_length=150, min_length=50):
    summarizer = pipeline("summarization", model="facebook/bart-large-cnn")
    return summarizer(text, max_length=max_length, min_length=min_length, do_sample=False)[0]['summary_text']

if __name__ == "__main__":
    file_name = get_uploaded_file()

    if file_name:
        text = extract_text_from_pdf(file_name, max_pages=3)
        processed_text = preprocess_text(text)
        
        summary = summarize_text(processed_text, max_length=150, min_length=50)
        
        print(f"\nSummary of '{file_name}':")
        print(summary)
    else:
        print("No PDF file found in the Colab environment.")
Files
script1_distilbart.py: Script using DistilBART-cnn for summarization.
script2_bart_large.py: Script using BART-large-cnn for summarization in a Colab environment.
Models Used
DistilBART-cnn: A smaller, faster version of BART, fine-tuned for summarization tasks.
BART-large-cnn: A large BART model fine-tuned on the CNN/DailyMail dataset for summarization.
