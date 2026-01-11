### 🧪 Model Benchmarking & Selection

Before selecting **Gemini 2.5 Pro**, we conducted a comparative analysis against other leading LLMs to ensure audit-grade financial accuracy.

| Model | Verdict | Observed Failure Mode |
| :--- | :--- | :--- |
| **Gemini 2.5 Pro** | ✅ **Selected** | Successfully adhered to the "Zero-Guessing" protocol. Returned "N/A" when data was missing rather than hallucinating. |
| **Llama 3 (Meta)** | ❌ Rejected | **Retrieval Adherence Failure:** Frequently ignored specific numbers in the retrieved text, substituting them with generic financial advice. |
| **DeepSeek-V3** | ❌ Rejected | **Arithmetic Hallucination:** "Invented" numbers in column-based extraction that looked correct but were factually wrong. |
| **OpenAI GPT-4o-mini** | ❌ Rejected | **Reasoning Deficit:** Lacked sufficient "Chain of Thought" depth. While fast, it frequently failed to synthesize multi-page context, reverting to shallow keyword matching rather than logic-based answering. |

#### 🎛️ Hyperparameter Optimization
We performed a grid search to identify the optimal decoding strategy for financial summarization.

| Parameter | Tested Values | Selected | Rationale / Experimental Finding |
| :--- | :--- | :--- | :--- |
| **Temperature** | 0, 0.7, 0.9 | **0.0** | **Enforced Determinism.** At 0.9, the model hallucinated external logic (e.g., blaming "market headwinds" for revenue drops when the text did not support it). 0.0 strictly limited the model to extraction only. |
| **Top-P** | 0, 0.5, 0.8 | **0.8** | **Readability Balance.** Top-P 0 produced overly robotic, disjointed sentences. 0.8 maintained accuracy while allowing for more natural sentence structures. |
| **Top-K** | 10, 40, 60 | **40** | **The "Sweet Spot."** Top-K 10 restricted vocabulary too aggressively, causing repetitive phrasing. Top-K 60 introduced "token noise" (irrelevant words). 40 provided the best balance for technical summarization. |
