# Supported Architectures

As of January 2026, Smolify primarily targets the **Google Gemma 3** family for edge deployment due to its superior reasoning-to-size ratio. See the [Gemma 3 Technical Report](https://storage.googleapis.com/deepmind-media/gemma/Gemma3Report.pdf).

### Target Architecture: Gemma 3 270M (IT)

All Foundry jobs currently distill into this specific architecture.

| Specification | Value |
| :--- | :--- |
| **Parameters** | 270 Million |
| **Precision** | FP16 / 4-bit Quantized |
| **Context Window** | 8k Tokens |
| **Architecture** | Transformer Decoder-only |
| **Attention Mechanism** | Grouped-query attention |
| **Hardware Req** | ~500MB RAM (Int4) |
| **Inference Speed** | ~45 tokens/sec (CPU) |

### Why 270M?
The 270M parameter class is the "Goldilocks" zone for **Single-Task Intelligence**. While it cannot write a symphony or code a website from scratch, it can be fine-tuned to perform specific tasks (classification, entity extraction, reformatting, IoT control) with 99% accuracy comparable to GPT-4, but at 1/1000th the cost.