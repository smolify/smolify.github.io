# Deploying with vLLM

While the **"Get Started"** guide shows how to run models using standard Python `transformers`, production environments often require higher throughput and an API server.

**vLLM** is a high-performance library for LLM serving. You can use it to turn your Smolify model into a drop-in replacement for the OpenAI API running locally or on your own server.

## 1. Installation

vLLM runs best on Linux machines with NVIDIA GPUs, though it supports AMD ROCm and Google TPU.

```bash
pip install vllm
```

## 2. Serving Your Model

Because Smolify models are hosted on Hugging Face and are **public by default**, serving them is a single-line command. You do not need API keys or login tokens unless you have manually set your Hugging Face repository to private.

Run the following command in your terminal:

```bash
# Syntax: vllm serve <your-username>/<your-project-name>

vllm serve my-username/smolified-clinical-scribe
```

vLLM will download your model weights automatically and start an API server at `http://localhost:8000`.

### Advanced Flags
Since Smolify models are ~270M parameters, they are incredibly lightweight.
*   **Memory:** If you have limited VRAM, vLLM will handle the small size easily.
*   **Context:** By default, it will utilize the model's max context window.

## 3. Connecting to the API

Once the server is running, you can interact with it using the standard OpenAI Python library. This allows you to integrate your custom sovereign model into existing apps simply by changing the `base_url`.

### Python Example

```python
from openai import OpenAI

# Point to your local vLLM server
client = OpenAI(
    base_url="http://localhost:8000/v1",
    api_key="smol" # vLLM requires a key string, but doesn't validate it by default
)

response = client.chat.completions.create(
    model="my-username/smolified-clinical-scribe",
    messages=[
        {"role": "system", "content": "You are a clinical scribe."},
        {"role": "user", "content": "Patient reports varying levels of pain in left knee."}
    ]
)

print(response.choices[0].message.content)
```

### cURL Example

You can also test the deployment directly from the command line:

```bash
curl http://localhost:8000/v1/chat/completions \
    -H "Content-Type: application/json" \
    -d '{
        "model": "my-username/smolified-clinical-scribe",
        "messages": [
            {"role": "system", "content": "You are a clinical scribe."},
            {"role": "user", "content": "Patient reports varying levels of pain in left knee."}
        ]
    }'
```

---

[**< Back to Documentation**](/docs/index)