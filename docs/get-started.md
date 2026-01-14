# Getting Started with Smolify

Smolify is a platform designed to "distill" massive reasoning engines into ultra-efficient, proprietary models. This guide walks you through defining, synthesizing, and training your specific model within the Foundry.

## Step 1: Authentication

The application sidebar handles all authentication.

1.  **If you have an API Key:** Enter it in the sidebar password field and click **Authenticate**.
2.  **If you are new:**
    *   Expand the **"No Key? Get one for free!"** section in the sidebar.
    *   Enter your email and click **Register**.
    *   Check your email (and spam folder) for your key.

*Once authenticated, you will see your current Credit Balance and Job History in the sidebar.*

## Step 2: Define Your Model Mission

You can define your model's behavior using one of three methods:

### Option A: Use a Trending Template (Fastest)
Click one of the **Trending Templates** pills at the top of the dashboard (e.g., "🏥 Clinical Scribe").
*   **Action:** This automatically pre-fills the Project Name, System Persona, and Description with battle-tested logic.

### Option B: Define from Scratch (Recommended)
Navigate to the **"✍️ Define Mission"** tab and fill in the following:
*   **Project Name (Required):** A unique name for your model (e.g., `Pirate-Email-Converter`).
*   **System Persona:** The "identity" of the AI (e.g., *"You are a salty pirate captain"*).
*   **Description:** A clear explanation of the task, inputs, and desired outputs (e.g., *"Convert professional emails into pirate speak"*).

### Option C: Upload Existing Data (Beta)
If you already have samples, navigate to the **"📄 Upload Training Data"** tab.
*   **Supported Formats:** CSV or JSON.
*   **Structure:** Your file should ideally have columns named `system`, `user`, and `assistant`.

## Step 3: Synthesize and Edit Data

1.  Click the **✨ Synthesize Preview** button (or verify your uploaded data).
2.  The app will generate a preview table under **"🔎 Review Synthetic Data"**.
3.  **Edit Interactively:** This is a live data editor. You can click into any cell (User Input or Target Output) to fix errors or tweak the logic before training begins.

## Step 4: Choose Your Pipeline Power

This is where you decide how the synthesis and training are processed.

### 🏆 Option A: Managed Pipeline (Recommended)
**Cost:** 1 Credit (~$10) | **Status:** *Optimized*

This is the standard, high-performance path. By using Smolify Credits, you get:
*   **Zero Configuration:** No need to manage external API keys or cloud consoles.
*   **Guaranteed Throughput:** We handle all rate limits and API negotiation with the teacher models.
*   **Production Quality:** Uses our optimized, high-tier inference endpoints for better synthetic data quality.

*To use this, simply click **Initialize Foundry Pipeline**. If you are low on credits, click the "Purchase Credits" link in the app.*

### 🛠️ Option B: Self-Managed / BYOK
**Cost:** Free | **Status:** *Manual Configuration*

If you prefer to manage your own infrastructure, you can bring your own keys. Note that you are responsible for your own API rate limits and quotas.
1.  Expand **"⚙️ Advanced Options"**.
2.  Enter your **Gemini API Key** in the designated field.
3.  *Note: Synthesis speed will depend on the tier of the key you provide.*

## Step 5: Advanced Hosting (Optional)

By default, models are hosted on the public `smolify` Hugging Face organization. To push to your own private repository:
1.  Expand **"⚙️ Advanced Options"**.
2.  Enter your **HF Write Token** and **Username/Org**.

## Step 6: Initialize Distillation

1.  Check the **Cost Card** to ensure you are using the desired method (Credits vs. Free Mode).
2.  Click **Initialize Foundry Pipeline**.
3.  **Monitor Status:** The app will display a "Foundry Status" log. You can watch as the system synthesizes the full corpus and trains the model.

## Step 7: Inference & Usage

Once the status changes to **Distillation Complete**, two links will appear:
*   **📦 Open Model:** Links to the Hugging Face Model card.
*   **📄 Open Dataset:** Links to the synthetic dataset used for training.

### How to run your model
Navigate to the **Open Model** link. Copy the Python snippet provided in the Model Card and run it in a GPU environment (like Google Colab) or in your local CPU (use vLLM).
