# LazyModels

**LazyModels** is a lightweight, zero-hassle utility for lazy-loading HuggingFace Transformers **and** SentenceTransformer models with automatic memory management on **CPU and GPU**.

### ✅ Install

```bash
pip install lazymodels
```

---

## 🚀 Features

* 🔄 **Lazy loading** of models by name (nothing is loaded until you call it)
* 🧠 **Smart task detection**: causal-lm, seq2seq, token classification, etc.
* 📦 Supports **HuggingFace Transformers** *and* **SentenceTransformers**
* 🧼 **Auto-unloading** of older models when memory limit is hit
* 🧠 **Device-aware** (CPU/GPU auto-detection)
* ⚡ Works in **1 line of code**
* 

---

## 🧪 Example

```python
from lazymodels import lazy_model_transformer

# Automatically loads a SentenceTransformer lazily
model = lazy_model_transformer("paraphrase-multilingual-MiniLM-L12-v2")

# Or a Transformers causal LM
gpt = lazy_model_transformer("gpt2")

# With tokenizer if needed
model, tokenizer = lazy_model_transformer("t5-small", tokenizer=True)
```

You can also access the global memory manager:

```python
from lazymodels import get_lazy_model_manager

print(get_lazy_model_manager().list_loaded())
```

---

## 💻 Memory Management

* Automatically detects available memory (CPU or GPU)
* Unloads oldest model when limit is exceeded
* If you don't specify memory limit, the manager uses **available memory at launch** (not full installed memory!)

---

## 🛠 Advanced Usage

```python
from lazymodels import get_lazy_model_manager
manager = get_lazy_model_manager()

# Manually register any custom loader
manager.register(
    name="custom::model",
    loader=lambda: YourModelClass(...),
    imports=["your_model_lib"]
)

# Load by name later
model = manager.get("custom::model")
```

---

## 📦 Dependencies

* `transformers`
* `torch`
* `sentence-transformers`
* `psutil`

---

## 🧠 Tip

Perfect for prototyping, memory-sensitive scripts, and large-model inference workflows.

---

MIT licensed. Made with ❤️ and pragmatism.
