# Getting Started with Smolify

Smolify is a platform designed to "distill" massive reasoning engines into ultra-efficient, proprietary models. This guide walks you through defining, synthesizing, and training your specific model within the Foundry.

## Step 1: Authentication

The application sidebar handles all authentication.

1.  **If you have an API Key:** Enter it in the sidebar field and click **Authenticate**.
2.  **If you are new:**
    *   Expand the **"No Key? Get one for free!"** section.
    *   Enter your email and click **Register**.
    *   Check your inbox (and spam) for your `sk-smolify-...` key.

*Once authenticated, you will see your current Credit Balance and Job History in the sidebar.*

## Step 2: Define Your Mission

You can define your model's behavior using one of three methods:

### Option A: Trending Templates (Fastest)
Click a **Trending Template** pill at the top of the dashboard (e.g., "🏥 Clinical Scribe").
*   **Action:** Automatically pre-fills the Project Name, System Persona, and Description with battle-tested prompts known to produce high-quality synthetic data.

### Option B: Define from Scratch (Recommended)
Navigate to the **"✍️ Define Mission"** tab:
*   **Project Name:** A unique handle (e.g., `Pirate-Email-Converter`).
*   **System Persona:** The "identity" of the AI (e.g., *"You are a salty pirate captain"*).
*   **Description:** A clear explanation of the task, inputs, and desired outputs.

### Option C: Upload Data (Beta)
Navigate to the **"📄 Upload Training Data"** tab.
*   **Format:** CSV or JSON.
*   **Schema:** Columns must map to `system`, `user`, and `assistant`.

## Step 3: Synthesize & Review

1.  Click **✨ Synthesize Preview**.
2.  The app will generate a sample table under **"🔎 Review Synthetic Data"**.
3.  **Live Editing:** This is an interactive table. Click any cell to correct logic errors before the full distillation process begins.

## Step 4: Select Pipeline Power

Smolify offers two distinct synthesis engines. Choose the one that fits your needs:

### 🏆 Option A: Managed Pipeline (1 Credit)
**Best for: Production-grade models, complex reasoning tasks.**

The Managed Pipeline utilizes a **Consensus Engine**. We aggregate outputs from various SOTA (State-of-the-Art) reasoning models (including OpenAI GPT-5, Anthropic Claude 4.5, and Google Gemini 3) to ensure the highest fidelity synthetic data.
*   **Zero Config:** We handle quotas and model routing.
*   **Higher Quality:** Multi-model verification reduces hallucinations in the training data.

### 🛠️ Option B: BYOK / Free Mode
**Best for: Prototyping, hobbyists, low-cost experiments.**

If you have your own credentials, you can run the foundry for free.
1.  Expand **"⚙️ Advanced Options"**.
2.  Enter your **Google Gemini API Key**.
3.  **Engine:** This pipeline strictly uses **Gemini 2.5 Flash**. While fast and efficient, it lacks the multi-model consensus of the managed tier.
4.  *Note: You are responsible for your own API rate limits.*

## Step 5: Hosting & Launch

By default, models are hosted on the public `smolify` Hugging Face organization. To push to your own account:
1.  Expand **"⚙️ Advanced Options"**.
2.  Enter your **HF Write Token** and **Username/Org**.

Click **Initialize Foundry Pipeline**. The system will now:
1.  Generate ~10,000 synthetic examples.
2.  Spin up an L4 GPU node.
3.  Fine-tune a **Gemma 3 (270M)** model on your data.

## Step 6: Inference

When the status changes to **Distillation Complete**, click the **📦 Open Model** link.

Your model is optimized for edge deployment. You can run it using `transformers`:

```python
from transformers import AutoProcessor, AutoModelForCausalLM

# Your specific model ID will be in the results link
model_id = "your-username/smolified-project-name" 

processor = AutoProcessor.from_pretrained(model_id, device_map="auto")
model = AutoModelForCausalLM.from_pretrained(model_id, dtype="auto", device_map="auto") # Runs on CPU!

message = [
    {"role": "system", "content": "Your System Prompt"},
    {"role": "user", "content": "Your Input"}
]

inputs = processor.apply_chat_template(message, add_generation_prompt=True, return_dict=True, return_tensors="pt")

out = model.generate(**inputs.to(model.device), pad_token_id=processor.eos_token_id, max_new_tokens=128)
output = processor.decode(out[0][len(inputs["input_ids"][0]):], skip_special_tokens=True)

print(output)
```