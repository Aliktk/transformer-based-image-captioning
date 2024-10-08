# Image Captioning using Transformers

**Author**: Ali Nawaz
**Date**: March 14, 2024

---

## Introduction

Hi Everyone, this article is focused on generating captions for any image using transformers. It provides all the details and procedures necessary to generate accurate captions for images.

You can find the entire code here: [GitHub Repository](github_link)

This article covers the following topics:

- Using Pre-trained Mobilenet Architecture to convert images into vectors that are fed to the cross-attention layer in the transformer decoder.
- Converting text into tokens and embeddings using TextVectorizer or other Tokenizers like BERT.
- Understanding Positional Embeddings, their purpose, and how transformers eliminate the sequential nature of RNNs.
- Global Self Attention, Causal Self Attention, and Cross Attention: when and how to use them.
- Creating and comparing the entire model architecture to previous ones.
- Model evaluation using Masked Loss, BLEU score, ROUGE score, and F-score.
- Visualizing the attention each word generates over different image segments.
- Dataset used: Flickr8k dataset (compatible with Flickr30k, MS-COCO).

---

## Positional Embeddings

Traditional models, like RNNs, process text sequentially to maintain word order. Transformers, however, lack this sequential nature, so positional encoding is applied to embed structural meaning.

Positional encoding vectors are added to embedding vectors, preserving order without distorting the embedding values.

### Image Vectorization

Here, Mobilenet-v3 (pretrained on ImageNet) is used to convert images into vectors. Resnet-50, Inception-Net, or other pretrained models can also be used. The top layers provide salient features, while lower layers capture detailed image features.

---

## Text Vectorization

Text conversion into tokens is an essential pre-processing step. In this project, the TensorFlow TextVectorization layer is utilized, with StringLookup for converting token IDs back to text.

### Reserved Tokens:

* `[START]`: Marks the start of a sentence.
* `[END]`: Marks the end of a sentence.
* `pad`: For sequence padding.
* `unk`: Represents unknown words.

---

## Attention Mechanism

Attention calculates the probability of context vectors (words or image segments) being associated with a word. For example, in the sentence:
 *“John was driving his car quite fast and ended up crashing it”* , the word *“it”* is closely related to  *“car”* .

### Types of Attention:

* **Cross Attention** : When query vectors (Q) come from a different source than key (K) and value (V).
* **Self Attention** : When Q, K, and V come from the same source.
* **Causal Self Attention** : Used during text generation to avoid looking ahead at future words.

## Loss and Accuracy Functions

* Masked loss is used to exclude padding tokens from loss calculations.
* BLEU, ROUGE, and F-score are applied to measure prediction quality.

### Key Points:

* **BLEU** : Precision-based metric.
* **ROUGE** : Recall-based metric.
* **F-Score** : Harmonic mean of BLEU and ROUGE.
* **Brevity Penalty** : Prevents artificially high BLEU scores for short predictions.

---

## Model Results

The model was trained for 150 epochs, using temperature-based random sampling for text generation. The F-1 score for unigrams achieved is 0.5, which is a good performance for this task.
