# Welcome to Smolify

**Intelligence, Distilled.**

Smolify is a foundry for **Domain Specific Language Models (DSLMs)**. We allow developers to distill the reasoning capabilities of massive, general-purpose models (like GPT-5, Claude 4.5, and Gemini 3) into ultra-compact, sovereign models (like Gemma 3 270M) that you own, host, and run anywhere.

### Why Distill?

*   **Sovereignty:** You own the weights. No API deprecations.
*   **Privacy:** Run locally on device (CPU/NPU). Data never leaves your perimeter.
*   **Cost:** Inference costs $0.
*   **Latency:** Sub-10ms response times on edge hardware.

### The Foundry Process

1.  **Define:** You describe a capability (e.g., "Clinical Scribe").
2.  **Synthesize:** We generate thousands of high-fidelity synthetic training examples.
3.  **Distill:** We fine-tune a specialized Nano-LLM using Neural Distillation.
4.  **Deploy:** You download the weights and run them via `transformers` or `vLLM`.

---

### Documentation Map

*   [**Get Started**](/docs/get-started): Launch your first distillation job in 5 minutes.
*   [**Core Concepts**](/docs/concepts): Understand Synthesis, Distillation, and DSLMs.
*   [**Model Architecture**](/docs/models): Technical specs of the Gemma 3-based output models.