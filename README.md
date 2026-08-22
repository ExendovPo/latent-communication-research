# Latent Communication Between Language Models

This repository contains experiments on transferring information between language models through hidden representations instead of natural-language messages.

The main question is:

**How do token position and transformer layer depth affect the transferability of information through latent communication between language models?**

## Setup

The experiments use:

- DistilGPT-2 as the source model
- GPT-2 as the receiving model in cross-model experiments
- a trainable linear adapter: `Linear(768, 768)`
- synthetic sentences containing objects and colors

A typical communication path is:

`DistilGPT-2 hidden state → linear adapter → latent embedding → GPT-2`

The language-model weights remain frozen. Only the adapter is trained.

## Experiments

The notebook includes:

- token position × transformer layer analysis
- experiments with two sentence templates
- adapter vs. no-adapter comparison
- transfer of object information
- cross-model latent communication
- robustness tests across multiple random seeds

## Main observations

The results show that transfer accuracy depends strongly on both token position and transformer layer.

Hidden states from the target token are generally easy to decode, while contextual information stored in later tokens varies substantially across layers.

For several contextual hidden states, direct transfer without an adapter produced 0% accuracy, while the trained adapter achieved high accuracy.

Cross-model experiments also showed that representations extracted from DistilGPT-2 can be transformed into useful latent inputs for GPT-2. Several selected configurations remained highly accurate across five random seeds.

## Limitations

The current experiments use small language models, synthetic data, and a relatively simple linear adapter. The results therefore describe this experimental setting and should not be treated as universal properties of transformer language models.

## Notebook

The full experimental notebook is available here:

[`latent_comm_final.ipynb`](latent_comm_final.ipynb)
