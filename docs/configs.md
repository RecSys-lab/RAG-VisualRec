# ⚙️ Configuration Schema

The pipeline is fully configurable through a single **config block**. This makes it easy to try out different experiments without changing the code — just edit the config and rerun.

---

## 🔑 Main Parameters

### 📂 Dataset

* `ml_latest_small` → MovieLens Latest Small
* `lfm360k` → Last.fm 360K

### 🧩 Embeddings

* `textual` → Text-only embeddings
* `visual` → Visual-only embeddings
* `audio` → Audio-only embeddings
* `fused_concat` → Concatenate all modalities
* `fused_pca` → PCA-based fusion (128-dim)
* `fused_cca` → CCA-based fusion (64-dim)
* `fused_avg` → Average embeddings

### 🤖 LLM Model

* `openai` → OpenAI Ada embeddings
* `sentence_transformer` → MiniLM or similar
* `llama3` → HuggingFace LLaMA model

### 👤 User Vector Strategy

* `random` → Random baseline (sanity check)
* `average` → Average of liked item embeddings
* `temporal` → Weighted by recency of interactions

### 🔎 Retrieval

* `N` → Number of nearest neighbors (default: `50`)

### 🎬 Recommendation

* `K` → Final top recommendations (default: `10`)
* `explainable` → `true/false` (include reasoning or not)

### ⚡ Runtime Settings

* `use_gpu` → Use GPU acceleration if available
* `seed` → Random seed for reproducibility
* `batch_size` → Batch size for embedding & retrieval

---

## 🛠 Example Config Block

```yaml
dataset: ml_latest_small
embeddings: fused_pca
llm_model: sentence_transformer
user_vector: temporal
retrieval:
  N: 50
recommendation:
  K: 10
  explainable: true
runtime:
  use_gpu: true
  seed: 42
  batch_size: 64
```

---

## ✅ Notes

* Default values are set to match the benchmarks used in experiments.
* Changing any config parameter requires **no code edits** — just update the block.
* This makes the system flexible for **rapid experimentation** and **extensibility**.