# From Unstructured Emails to Explainable Predictions: Automating Customer Support Ticket Escalation

Code repository for the paper "From Unstructured Emails to Explainable Predictions: Automating Customer Support Ticket Escalation"

## Authors

**Berat Furkan Kocak** (University of Padova, Italy, kocakberatfurkan@gmail.com)  
**Gyunam Park** (Eindhoven University of Technology, The Netherlands, g.park@tue.nl)

## Overview

This repository contains the implementation of an automated seven-stage pipeline that leverages large language models (LLMs) to extract structured features from customer support emails and employs explainable machine learning to predict the optimal timing of ticket creation within email conversations.

## Directory Structure

```
unstructured-emails-to-explainable-predictions/
│
├── .env                                          # Environment variables (API keys)
├── requirements.txt                              # Python dependencies
├── unstructured-emails-to-explainable-predictions.ipynb  # Main notebook
│
├── data/
│   └── sample_email_threads.json                # Sample email thread data
│
└── outputs/
    ├── selected_features.json                   # Selected features for analysis
    ├── stage1_initial_features.json             # Initial features from LLM
    ├── stage1_initial_features_validated.json   # Validated initial features
    ├── stage2_clusters_analysis.json            # Clustering analysis results
    ├── stage2_consolidated_features.json        # Consolidated feature schema
    ├── stage3_extracted_features.csv            # Extracted feature values
    ├── stage4_final_dataset.csv                 # Final structured dataset
    ├── stage6_model_comparison.png              # Model performance visualization
    ├── stage6_model_results.csv                 # Model comparison results
    └── stage7_active_learning_results.csv       # Active learning evaluation
```

## Sample Data

Due to privacy concerns related to real company and user data, we are sharing a synthetically-generated email thread dataset to ensure reproducibility. This dataset was created using large language models (LLMs) via the OpenRouter API to simulate realistic customer support interactions.

### Dataset Generation

The dataset was generated using a multi-model approach with automatic fallback, utilizing the following open-source and proprietary LLMs:

- `qwen/qwen3-235b-a22b` (free tier)
- `qwen/qwen-2.5-72b-instruct` (free tier)
- `x-ai/grok-4.1-fast` (free tier)
- `openai/gpt-oss-20b` (free tier)

The generation process simulated realistic customer support scenarios across various domains including:

- Software errors and database connectivity issues
- Equipment damage and repair needs
- Warranty claims and service requests
- Configuration and technical support issues
- Business-critical incidents requiring escalation

### Dataset Statistics

- **Total email threads:** 227
- **Emails per thread:** 2-6 (variably generated)
- **Total emails:** 873 individual emails

### Data Structure

Each thread contains:

- Thread metadata (ID, ticket requirement, ticket details)
- Email exchanges with sender information, timestamps, subjects, and body text
- Summary labels including issue type, urgency, business impact, and technical complexity (The summary field is not passed to the LLMs during feature extraction.)

## Setup Instructions

### 1. Create a Virtual Environment

Create and activate a Python virtual environment:

```bash
# Windows
python -m venv venv
venv\Scripts\activate

# macOS/Linux
python3 -m venv venv
source venv/bin/activate
```

### 2. Install Dependencies

Install all required libraries using the provided `requirements.txt`:

```bash
pip install -r requirements.txt
```

**Note:** Alternatively, you can install dependencies directly within the Jupyter notebook by running cells that contain installation commands.

### 3. Configure Environment Variables

**Important:** The pipeline uses LLMs via OpenRouter API. You must obtain an API key from [OpenRouter](https://openrouter.ai/) and add it to the `.env` file before running the notebook.

Create a `.env` file in the root directory (if not already present) and add your OpenRouter API key:

```bash
OPENROUTER_API_KEY=your_api_key_here
```


### 4. Run the Notebook

Open the main notebook (either through Jupyter or any other environment) and execute the cells sequentially to reproduce the pipeline.

**IMPORTANT** 
After Stage2 is completed, human expert MUST:
1. Review the obtained clusters under outputs/stage2_consolidated_features.json 
2. Create a selected_features.json under outputs directory by choosing the interesting clusters.
Selected features are used in Stage3 for extracting corresponding values for each email.  

