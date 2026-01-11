### 🛡️ Reliability & Failure Mitigation

To ensure system stability in a corporate environment, we mapped potential failure modes and implemented hard-coded safety valves.

| Risk Area | Potential Failure | Mitigation Strategy Implemented |
| :--- | :--- | :--- |
| **Vector Database** | **Metadata Overflow:** A single dense table >40KB crashes the Pinecone ingestion pipeline. | **Auto-Truncation Logic:** A `truncate_to_bytes` function automatically cuts metadata to 39KB before upserting, preventing pipeline stalls. |
| **API Limits** | **429 Resource Exhausted:** Uploading large Annual Reports triggers Google Vertex AI rate limits. | **Exponential Backoff:** Implemented a smart retry loop that sleeps (up to 60s) when hitting Quota-Per-Minute limits. |
| **OCR Precision** | **"The 8 vs 3 Typo Problem":** Standard OCR misreads blurry financial digits. | **Vision-First Ingestion:** Bypassed text-layer extraction; used Gemini Vision to "read" the page as an image (300 DPI), improving digit accuracy by ~15%. |
