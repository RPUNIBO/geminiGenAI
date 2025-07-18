# 🔮 Google AI Studio + Gemini API Integration

This repository demonstrates how to connect Google AI Studio with Colab using the Gemini Pro 2.5 API. It walks through setting up API keys, listing available models, configuring safety and generation settings, and generating AI content via the `generate_content()` method.

---

## 📌 Prerequisites

- A Google Cloud account
- Access to [Google AI Studio](https://makersuite.google.com/)
- Google Colab
- Gemini API key

---

## 🚀 Setup Instructions

### 🔑 Step 1: Create a Google Cloud Project

1. Visit [Google AI Studio](https://makersuite.google.com/)
2. Create a new project.
3. Enable the **Generative Language API**.
4. Generate an API key. You will get a key like:


---

### 🤖 Step 2: Connect in Google Colab

1. Open a new notebook in [Google Colab](https://colab.research.google.com/)
2. In the left panel, click on the 🔐 **Secrets** tab.
3. Add a new secret:
- Name: `google_api_key`
- Value: (Paste your actual API key here)

---

### 📦 Step 3: Install and Import Dependencies

```python
!pip install -q google-generativeai
import google.generativeai as genai
import os

Step 4: Authenticate
python
Copy
Edit
from google.colab import userdata
genai.configure(api_key=userdata.get('google_api_key'))

Step 5: List Available Models
python
Copy
Edit
for model in genai.list_models():
    print(model.name)
✅ Output should include models like:

models/gemini-pro

models/gemini-1.5-pro

models/gemini-1.5-pro-latest

 Step 6: Load Gemini 2.5 Pro
python
Copy
Edit
model = genai.GenerativeModel('gemini-1.5-pro-latest')

Safety & Generation Configurations
1. generation_config()
Set temperature, max tokens, top-p, top-k etc.

python
Copy
Edit
gen_config = genai.types.GenerationConfig(
    temperature=0.7,
    top_p=0.95,
    top_k=40,
    max_output_tokens=512
)
2. safety_settings()
Prevents harmful or biased outputs

python
Copy
Edit
safety_settings = {
    "HATE": "BLOCK_LOW_AND_ABOVE",
    "VIOLENCE": "BLOCK_LOW_AND_ABOVE",
    "SEXUAL": "BLOCK_LOW_AND_ABOVE",
    "HARASSMENT": "BLOCK_LOW_AND_ABOVE"
}
🧠 Generate Text using generate_content()
python
Copy
Edit
response = model.generate_content(
    "Explain the concept of entropy in simple terms.",
    generation_config=gen_config,
    safety_settings=safety_settings
)
print(response.text)
🧩 Advanced: Chunked Response Display
python
Copy
Edit
for chunk in response:
    print(chunk.text)
✅ Output Safety Check
python
Copy
Edit
print(response.prompt_feedback)
If blocked=True, your input was flagged as unsafe. Review safety_ratings for the category (e.g., HATE, HARASSMENT, etc.)

🧪 Utility Function Example
Replace . with * in generated text:

python
Copy
Edit
def to_markdown(text):
    return text.replace(".", "*")
✅ Confirmation
A successful API call proves your setup is working.

📌 Notes
Gemini models are evolving — always check model availability with list_models().

Keep your API keys safe and do not share them publicly.

Make sure to handle exceptions and safety feedback properly in production.