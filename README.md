# Semantic-NLP-Filtering-and-Classification-of-Virology-Epidemiology-Research-Papers

## Overview

This repository contains a system for filtering, classifying, and extracting methods from a large dataset of academic papers related to virology and epidemiology. The goal of this project is to identify and categorize papers that implement deep learning techniques, improving the speed and accuracy of literature review for researchers interested in the application of neural network-based approaches in these fields.

The solution comprises three main components:
1. **Semantic Filtering** of relevant deep learning papers.
2. **Methodology Classification** to categorize each paper by the type of deep learning technique applied (e.g., text mining, computer vision, both or other).
3. **Method Extraction** to identify and report specific deep learning models and approaches used in each paper.

## Dataset

The dataset, containing 11,450 records, was sourced from a keyword-based search on PubMed. Each record includes the paper's title, abstract and other metadata. Both title and abstract are used for filtering and classification.

### Final Dataset Statistics

The results after filtering and classification:

- **Total Relevant Papers Identified**: 3,656
- **Classification Breakdown**:
  - **Text Mining**: 854 papers
  - **Computer Vision**: 282 papers
  - **Both (Text Mining and Computer Vision)**: 311 papers
  - **Other**: 2209 papers

### Extraction of Specific Methods

The method extraction process identified the most common deep learning methods, with the following top methods:

- **Machine Learning Model**: 1063
- **Deep Neural Networks**: 506
- **CNN**: 246
- **Large Language Model**: 196
- **Artificial Neural Network**: 124

## System Components and Approach

### 1. Semantic NLP Filtering

#### NLP Technique Used
For filtering papers relevant to deep learning in virology/epidemiology, **semantic natural language processing (NLP)** has been used, specifically the 'SentenceTransformer' model ('all-MiniLM-L6-v2'). This approach leverages contextual embeddings to measure the semantic similarity between each paper’s content and a set of predefined deep learning-related keywords. By using embeddings, this method moves beyond simple keyword matching, understanding the context in which terms are used.

#### Why Semantic Filtering over Keyword-Based Filtering?
While keyword-based filtering can quickly identify exact matches, it fails to account for variations in phrasing or synonyms. Semantic filtering allows for a more accurate representation of the paper’s content, capturing relevant papers that might use synonymous terms or slightly different language to describe deep learning techniques. This technique helps reduce false negatives, ensuring more comprehensive results for researchers.

#### Filtering Process
Each paper’s title and abstract are combined, and the resulting text embedding is compared to embeddings of relevant keywords. Papers with a cosine similarity score above a threshold (0.35) are deemed relevant.

### 2. Classification by Method Type

After identifying the relevant papers, I categorize each one based on its primary methodology into the following groups:

- **Text Mining**: Papers using NLP techniques.
- **Computer Vision**: Papers using image-processing or visual recognition models.
- **Both**: Papers combining text mining and computer vision.
- **Other**: Papers using deep learning techniques that don’t fall into the above categories.

#### Classification Method
I defined the keywords for each category and use embedding-based cosine similarity to classify papers. A paper is classified into the category with the highest similarity score, provided it exceeds specific threshold of 0.3. This embedding-based approach captures the semantic relevance to each category rather than relying on specific words alone.

### 3. Extraction of Deep Learning Methods

For each relevant paper, specific deep learning method(s) discussed will be extracted. I created embeddings for keywords representing various neural network architectures (e.g., “CNN,” “LSTM,” “transformer”) and compared each paper’s embedding to identify the most relevant method.

#### Extraction Process
- For each paper, I calculate the cosine similarity between the paper’s embedding and each method keyword embedding.
- The method with the highest similarity score above a threshold of 0.3 is selected as the main method used in the paper.
- This approach allows us to detect methods even when the specific terminology differs slightly from our predefined keywords.

## Usage

1. **Setup**:
   - Clone the repository and install the necessary packages (All necessary packages are in requirements.txt file). Please run the command "pip install -r requirements.txt"
   - Load the dataset into the system ('preprocessed_data.csv').

2. **Running the Code**:
   - To filter papers, run the filtering function to generate a list of relevant papers.
   - Apply the classification function to categorize the filtered papers.
   - Finally, run the extraction function to identify the specific deep learning methods mentioned.

3. **Output**:
   - The filtered dataset, with classifications and extracted methods, is saved to `research_papers_classification.csv` for further analysis.

## Evaluation and Output Summary

- **Effectiveness**: The system has been evaluated based on its ability to identify relevant deep learning papers with high accuracy compared to keyword-based filtering.
- **Output Files**:
  - 'filtered_papers.csv': Contains papers deemed relevant to deep learning in virology/epidemiology.
  - 'methodType_classified_papers.csv': Contains classified papers with a method type label.
  - 'research_papers_classification.csv': The final dataset with relevant papers, their classification, and extracted deep learning methods.
