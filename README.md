# **Fine-tuning a Large Language Model for German-to-French Translation**

## **About The Project**

This project focuses on fine-tuning a general-purpose Large Language Model (LLM) for the specific task of translating text from German to French. The core of this exploration is to evaluate the effectiveness of using a synthetically generated dataset versus a standard benchmark dataset for the fine-tuning process.  
The project uses the Qwen2-1.5B model and employs Low-Rank Adaptation (LoRA) for parameter-efficient fine-tuning. The performance of different models is evaluated using the BLEU score.
This project was done as part of my portfolio exam.

## **Getting Started**

To get a local copy up and running, follow these simple steps.

### **Prerequisites**

This project uses Python and several libraries. You will need to have Python installed on your system.

### **Installation**

1. Clone the repo

2. Install the required packages:  
   pip install datasets transformers accelerate evaluate peft bitsandbytes trl groq

3. **API Keys:** You will need API keys for Weights & Biases (WANDB\_API\_KEY) and Groq (GROQ\_API\_KEY). The notebook is set up to either read them from your environment variables or prompt you to enter them manually.

## **Usage**

The primary file for this project is the Jupyter Notebook genAI.ipynb. You can run the cells sequentially to reproduce the results.  
The notebook covers the following steps:

1. **Load Dataset**: Loads the Flores-200 dataset and prepares it for training and testing.  
2. **Load Pre-trained Model**: Loads the base Qwen2-1.5B model (Model A).  
3. **Evaluate Base Model**: Tests the base model's translation performance.  
4. **Fine-tune with Benchmark Data**: Fine-tunes the base model on the Flores-200 training set to create Model B.  
5. **Generate Synthetic Data**: Uses a larger LLM via the Groq API to generate a new synthetic dataset (Dataset B).  
6. **Fine-tune with Synthetic Data**: Fine-tunes the base model on the synthetic dataset to create Model C.  
7. **Fine-tune with Combined Data**: Fine-tunes the base model on a combination of the benchmark and synthetic datasets to create Model D.  
8. **Evaluate and Plot Results**: Compares the BLEU scores of all models and visualizes the performance.

## **Methodology**

### **Dataset**

The **Flores-200 dataset** from Meta AI was chosen as the benchmark dataset. It's a standard for NLP and translation tasks and provides a sufficient number of German-to-French sentence pairs. A subset of 1000 sentence pairs was used, split into an 80-20 train-test ratio.  
A synthetic dataset was generated using a more advanced model (Llama3-70B via Groq API) to create new, diverse, and accurate translation pairs.

### **Model**

**Qwen2-1.5B** was selected as the base model. Its relatively small size makes it suitable for fine-tuning on consumer hardware (like Google Colab's free tier), and it has strong performance in multi-lingual tasks.

### **Fine-tuning Approach**

**Low-Rank Adaptation (LoRA)** was used for fine-tuning. LoRA is a parameter-efficient fine-tuning (PEFT) method that significantly reduces the number of trainable parameters, making the process computationally efficient without sacrificing much performance.

### **Evaluation Metric**

The **BLEU (Bilingual Evaluation Understudy)** score was used to evaluate the quality of the translations. BLEU is a standard metric in machine translation that measures the similarity between a machine's output and high-quality human reference translations.

## **Results**

The fine-tuning process yielded the following BLEU scores for the different models:

| Model | Description | BLEU Score |
| :---- | :---- | :---- |
| **A** | Base Qwen2-1.5B Model | 0.210 |
| **B** | Fine-tuned on Benchmark Data | 0.211 |
| **C** | Fine-tuned on Synthetic Data | 0.211 |
| **D** | Fine-tuned on Combined Data | 0.208 |

The results indicate that the base model was already quite proficient at German-to-French translation. Fine-tuning on either the benchmark or synthetic data alone provided a marginal improvement. Interestingly, combining the datasets led to a slight decrease in performance, possibly due to inconsistencies introduced by mixing real and synthetic data.

## **Ethical Considerations**

When using language models for translation, it's important to be aware of the following ethical considerations:

* **Bias and Fairness**: Models can perpetuate biases present in their training data, leading to inaccurate or stereotypical translations.  
* **Privacy**: Sensitive information within the training data could potentially be exposed.  
* **Misuse Potential**: Translation models could be used for malicious purposes, such as creating disinformation.  
* **Transparency**: Over-reliance on machine translation without understanding its limitations can be risky, especially in critical contexts.  
* **Cultural Sensitivity**: Direct translations may fail to capture cultural nuances, leading to misunderstandings.
