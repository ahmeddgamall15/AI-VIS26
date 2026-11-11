# AI-VIS26 – AI and Visualization Lab

## Project Overview

This project investigates how a Convolutional Neural Network (CNN) behaves when classifying clothing images from the Fashion-MNIST dataset.

Our main goal in Phase 1 is to understand the model's mistakes, particularly why some shirts are incorrectly classified as coats.

We also compare two approaches to analyzing the model: a human-only approach and an AI-assisted approach using ChatGPT.

## Model and Dataset

- **Model:** Convolutional Neural Network (CNN)
- **Dataset:** Fashion-MNIST
- **Test data:** 10,000 grayscale images (28 × 28 pixels)
- **Categories:** 10 clothing categories
- **Model weights:** `fashion_cnn.pth`

Both pairs use the same dataset and trained model for their investigations.

## Phase 1 – Model Behavior

Our analysis focuses on the Shirt-to-Coat classification problem.

We use confusion matrices, image comparisons, bar charts, and probability visualizations to understand the model's behavior.

### Pair 1 – Human-only Approach

This approach investigates whether average brightness around the sides of shirts is related to the model's classification mistakes.

The analysis compares shirts with lower and higher side brightness.

### Pair 2 – AI-assisted Approach

This approach uses ChatGPT to support the analysis and investigate a similar question using side-pixel coverage.

It also explores prediction confidence through softmax probabilities and checks whether overall image brightness could explain the observed patterns.

## Repository Contents

- **Phase 1 notebooks:** Analysis code and visualizations from both pairs.
- **fashion_cnn.pth:** Trained CNN model weights.
- **ai-interactions/:** Documentation of Generative AI usage.
- **ai_reflection_midpoint.md:** Reflection on the use of Generative AI.
- **team-info.json:** Group member information.
- **workload.json:** Distribution of work among group members.

## Phase 1 – Progress Presentation

Our Phase 1 progress presentation summarizes the work of both pairs, highlights the main findings, and compares the human-only and AI-assisted approaches.

**Video Presentation:** [Watch our Phase 1 presentation](https://youtu.be/sk1LoQmr6ag)

## Phase 2 – Model Understanding

In Phase 2, we will investigate what the CNN has learned internally, using visualization and explanation techniques.

The two pairs will switch their AI-assisted and human-only roles.
