### **`openai>=1.30.0` Python Library Guide**

The `openai` Python package (version `1.30.0` and above) provides an interface to OpenAI's **GPT-4, DALL·E, Whisper, and other AI models** via the OpenAI API.

---

## **1️⃣ Install `openai>=1.30.0`**

```bash
pip install openai>=1.30.0
```

✅  **Dependencies** : Ensure you have Python `>=3.7`.

---

## **2️⃣ Basic Usage: ChatGPT API**

```python
import openai

openai.api_key = "your-api-key"

response = openai.ChatCompletion.create(
    model="gpt-4",
    messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {"role": "user", "content": "Explain OpenAI API in simple terms."}
    ]
)

print(response["choices"][0]["message"]["content"])
```

✅ **Use Case:** Queries GPT-4 and retrieves responses.

---

## **3️⃣ Image Generation (DALL·E)**

```python
response = openai.Image.create(
    model="dall-e-3",
    prompt="A futuristic city skyline at sunset",
    n=1,
    size="1024x1024"
)

image_url = response["data"][0]["url"]
print(image_url)
```

✅ **Use Case:** Generates AI-powered images.

---

## **4️⃣ Speech-to-Text (Whisper)**

```python
audio_file = open("speech.mp3", "rb")

response = openai.Audio.transcribe(
    model="whisper-1",
    file=audio_file
)

print(response["text"])
```

✅ **Use Case:** Converts speech to text.

---

## **5️⃣ Fine-tuning a Custom Model**

```python
response = openai.FineTuning.create(
    model="gpt-4",
    training_file="file-id"
)
print(response)
```

✅ **Use Case:** Trains a GPT model on custom data.

---

## **6️⃣ Streaming Responses (Real-time Output)**

```python
response = openai.ChatCompletion.create(
    model="gpt-4",
    messages=[{"role": "user", "content": "Tell me a joke."}],
    stream=True
)

for chunk in response:
    print(chunk["choices"][0]["delta"].get("content", ""), end="")
```

✅ **Use Case:** Streams responses token by token.

---

## **7️⃣ Interview Questions on `openai`**

### **1️⃣ Basic Questions**

✔ What is the OpenAI API, and how is it used?

✔ How do you authenticate API requests?

✔ What models are available in OpenAI's API?

### **2️⃣ Advanced Questions**

✔ How does `openai.ChatCompletion.create()` work?

✔ How do you handle  **rate limits and errors** ?

✔ What are  **best practices for fine-tuning GPT models** ?

✔ How does OpenAI's **streaming API** improve response times?

---

## **🚀 Next Steps**

Would you like an example with **FastAPI integration** or  **LangChain support** ? 🎯
