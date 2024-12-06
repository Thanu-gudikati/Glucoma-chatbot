# Glaucoma Chatbot

This Glaucoma Chatbot answers glaucoma-related questions by using two different embedding models: **BioBERT** and **BioWordVec**. The chatbot returns two responses—one from each model—along with confidence scores for each answer. This project demonstrates how to use pretrained embeddings to match questions and answers in a conversational chatbot.

## Table of Contents
- [Features](#features)
- [Installation](#installation)
- [Setup](#setup)
- [Usage](#usage)
- [Troubleshooting](#troubleshooting)
- [Acknowledgments](#acknowledgments)

---

## Features
- **BioBERT Model** for biomedical question-answering tasks.
- **BioWordVec Model** for fast and efficient word embeddings in the biomedical domain.
- **Cosine Similarity** to find the most relevant answer for user questions.
- **Confidence Scores** for BioBERT and BioWordVec responses to evaluate answer relevance.

## Installation

### Prerequisites
- Python 3.7+
- [PyTorch](https://pytorch.org/get-started/locally/) (compatible with your CUDA setup if using GPU)
- Required Python packages:
  - `transformers`
  - `gensim`
  - `numpy`
  - `pandas`
  - `scikit-learn`

### Step-by-Step Installation

1. **Clone the repository** (or download the code files directly):
    ```bash
    git clone <repository-url>
    cd <repository-folder>
    ```

2. **Create a virtual environment** (optional but recommended):
    ```bash
    python3 -m venv glaucoma-chatbot-env
    source glaucoma-chatbot-env/bin/activate  # For Linux/Mac
    glaucoma-chatbot-env\Scripts\activate     # For Windows
    ```

3. **Install the required packages**:
    ```bash
    pip install torch transformers gensim numpy pandas scikit-learn
    ```

4. **Download the BioBERT model**:
    The BioBERT model will be downloaded automatically when you run the code, as it's specified by the Hugging Face model ID `dmis-lab/biobert-base-cased-v1.1`.

5. **Download the BioWordVec model**:
    Place the BioWordVec model file [`bio_embedding_intrinsic`](https://figshare.com/articles/dataset/Improving_Biomedical_Word_Embeddings_with_Subword_Information_and_MeSH_Ontology/6882647) in the same folder as your project files. Ensure it’s in the correct format (binary).

6. **Dataset**:
    Ensure you have the file `Combined_Dataset.xlsx` containing the Q&A data in the project directory. This dataset should have columns named exactly as `Question` and `Answer`.

## Setup

1. **Verify Data Format**:  
    Ensure that `Combined_Dataset.xlsx` has columns named exactly `Question` and `Answer`.

2. **Precompute Embeddings**  
   Run the main script to precompute embeddings, which will save them to a pickle file (`precomputed_embeddings.pkl`) for faster future use.

    ```bash
    python chatbot.py
    ```

## Usage

1. **Run the Chatbot**
    ```bash
    python chatbot.py
    ```

2. **Interact with the Chatbot**
   - The chatbot will prompt you to ask questions related to glaucoma.
   - Type your question and press **Enter**.
   - The chatbot will respond with answers from both BioBERT and BioWordVec, along with confidence scores.

3. **Exit the Chatbot**
   - Type `exit` to close the chatbot.

### Sample Chat
```plaintext
Hey there..! I'm Glaucoma Chatbot!
You can ask any question related to glaucoma or type 'exit' to stop.

Your question: What are the symptoms of glaucoma?
--- BioBERT Response ---
Matched Question: What are the primary symptoms of glaucoma?
Answer: The primary symptoms include blurred vision, eye pain, etc.
Confidence: 0.85

--- BioWordVec Response ---
Matched Question: Symptoms of glaucoma?
Answer: Blurred vision, headaches, and seeing halos.
Confidence: 0.82

Your question: exit
Thank-You!
```
## Troubleshooting

### Common Issues and Fixes

- **BioWordVec Model Not Found**: 
    - Ensure that the `bio_embedding_intrinsic` model file is downloaded and placed in the project directory. The file should be in **binary format** (check that the extension is correct if you have modified or downloaded the file manually).

- **CUDA or GPU Errors**:
    - If you encounter issues with CUDA (e.g., if using a GPU-enabled setup), ensure your **PyTorch version** is compatible with your **CUDA version**. You can verify compatibility and find specific installation instructions for PyTorch [here](https://pytorch.org/get-started/locally/).
    - Alternatively, to run on CPU, specify device configuration in the code by modifying `torch.device("cpu")`.

- **Precomputed Embeddings Not Found**:
    - If you see an error about missing `precomputed_embeddings.pkl`, this may indicate that the embeddings file was not generated. Rerun the main script to ensure that embeddings are correctly precomputed and saved.

- **Data File Issues**:
    - Ensure `Combined_Dataset.xlsx` has the columns `Question` and `Answer` exactly as labeled. Any mismatch in column names could lead to errors during data loading and processing.
    - Verify the file path if you're encountering a "file not found" error.

- **Library Import Errors**:
    - If any imports fail, recheck that all dependencies are installed as specified in the **Installation** section, and make sure you’re working within your virtual environment if one was created.

### Additional Help
For any issues not addressed here, consult the documentation for [transformers](https://huggingface.co/docs/transformers), [gensim](https://radimrehurek.com/gensim/), and [PyTorch](https://pytorch.org/), or file an issue on the GitHub repository if you believe the issue is specific to this project.

---

## Acknowledgments

This project relies on the hard work and contributions of the biomedical NLP community. Special thanks to:

- **BioBERT** ([DMIS Lab](https://github.com/dmis-lab/biobert))  
   BioBERT is a transformer model fine-tuned on biomedical data, specifically developed to improve biomedical question-answering and related NLP tasks.
  
- **BioWordVec** ([NCBI NLP](https://github.com/ncbi-nlp/BioWordVec))  
   BioWordVec provides word embeddings derived from PubMed and other biomedical sources, allowing for effective handling of specialized biomedical vocabulary.

Both models have greatly enhanced the ability to deliver accurate, context-aware responses in biomedical domains, and this chatbot wouldn't be possible without these advancements.

---
