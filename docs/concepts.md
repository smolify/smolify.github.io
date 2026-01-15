# Core Concepts

### Neural Distillation
Neural Distillation is the process of transferring knowledge from a large "Teacher" model (e.g., a 1 Trillion parameter model) to a small "Student" model (e.g., 270 Million parameters).

Smolify automates this by:
1.  **Prompting the Teacher:** We ask the large model to generate thousands of diverse, high-quality examples of a specific task.
2.  **Filtering:** We clean the data to remove noise.
3.  **Supervised Fine-Tuning (SFT):** We train the Student model to mimic the Teacher's outputs.

### Sovereign Models
A Sovereign Model is an AI asset that you fully own.
*   **Platform Independence:** It does not rely on an API connection to OpenAI or Google.
*   **Fixed Behavior:** The model won't change or get "lazy" because a provider updated their backend.
*   **Portability:** You can put it on a USB drive, a drone, or an air-gapped server.

### The "Smol" Advantage
We specialize in **Micro-LLMs**.
*   **Traditional LLMs:** 7B to 70B parameters. Requires 16GB+ VRAM (expensive GPUs).
*   **Smolify Models:** ~270M parameters. Requires <1GB RAM. Runs on Raspberry Pi, mobile phones, and web browsers.

---

[**< Back to Documentation**](/docs/index)