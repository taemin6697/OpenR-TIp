
# 🚀 OpenR-Tip: A Benchmark Dataset for Service Evaluation Research

![OpenR-Tip Logo](logo.png)

## 📌 Overview
**OpenR-Tip** (Open Reddit-based Tipping Scenarios) is a high-quality benchmark dataset designed to address the lack of publicly available datasets containing paired real-world service scenarios and their corresponding tip amounts[cite: 339, 340]. 

This dataset enables the evaluation of Large Language Models (LLMs) and Vision-Language Models (VLMs) in their ability to perform complex service quality reasoning and predict economic outcomes (tip percentages)[cite: 16].

## 🧩 Dataset Composition
Each sample in the final dataset consists of a multimodal tuple:
* **Video Caption**: Objective textual evidence of staff behavior generated from raw narratives[cite: 15, 178].
* **User Review**: Manually authored subjective customer feedback based on sanitized raw text[cite: 15, 409].
* **Star Rating**: Customer-assigned satisfaction score (1–5 scale)[cite: 153].
* **Google Review**: External contextual data matched to similar real-world establishments via Proxy Matching[cite: 163, 412].
* **Fair Tip Percentage**: Target label (%) ethically validated and corrected by human annotators[cite: 414, 415].

---

## 🛠 Data Construction Pipeline
The dataset was constructed using a multi-stage, LLM-assisted pipeline with strict human supervision to prevent data leakage[cite: 341, 392].

1. **Data Collection**: 2,000 samples collected from Reddit (e.g., r/TalesFromYourServer)[cite: 343, 387].
2. **Filtering**: Mistral-3.1 was used to retain posts with clear situational context and specific tip percentages[cite: 394, 395].
3. **Consistency Check**: Contradictory samples were eliminated to ensure high-quality ground truth[cite: 397, 398].
4. **Human-Supervised Refinement**: Masking tip info, generating supervised captions (Gemini 3 Flash), and manual blind annotation of reviews[cite: 402, 403, 410].
5. **Fair Tip Correction**: Outliers were adjusted by human annotators to ensure ethical and logical consistency (e.g., correcting 0% tips for excellent service)[cite: 415, 418].

---

## 📝 Data Format Example (Refined Dataset)
Below is a representative sample from the `reddit_tip_dataset.json`:

```json
{
  "id": "aeqpbu",
  "search_keyword": "generous tip",
  "subreddit": "TalesFromYourServer",
  "virtual_situation_caption": "Kiosk camera shows a small 12-table dining room... One server works alone on the floor, moving continuously... speaking briefly and apologetically about longer wait times...", 
  "human_user_review": "The service was an absolute disaster. We waited forever... the server was completely incompetent.",
  "human_star_rating": 1,
  "google_review": "Google Review #2: It seemed like the staff was understaffed and overwhelmed. I felt bad for the poor server...",
  "human_tip_percentage": 3.33,
  "situation_fair_tip": 12.4, // Ethically corrected label
  "text_content": "This happened earlier this week. I work for a small mom and pop store..." // Original Reddit source
}


