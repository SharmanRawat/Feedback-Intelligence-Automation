# Feedback Intelligence Automation Engine 🤖⚡

[![n8n](https://img.shields.io/badge/n8n-v1.0+-blue)](https://n8n.io)
[![AI](https://img.shields.io/badge/AI-Groq%20Llama%203.3-green)](https://groq.com)
[![Tech](https://img.shields.io/badge/Stack-Google%20Sheets%20%2B%20Gmail-orange)](https://github.com/)

An AI-powered n8n workflow that automatically triages event feedback, classifies sentiment and urgency using an LLM, and routes responses to coordinators and students with zero manual sorting.

## 📸 Project Showcase

| **Automation Canvas** | **Email Output Example** |
| :---: | :---: |
| ![Workflow Canvas](assets/Screenshot_From_2026-07-23_02-23-31.png) | ![Action Plan Email](assets/Screenshot_From_2026-07-23_02-33-45.png) |

## 🚀 Key Features
- **Instant AI Sentiment Analysis:** Classifies feedback into Positive, Negative, Neutral, or Mixed using Groq's Llama 3.3.
- **Dynamic Urgency Routing:** Assigns a 1-5 urgency score and maps the issue to the correct department (Venue, IT, Speaker, etc.).
- **Auto-Generated Action Plans:** Creates an immediate "Action Plan" and a "Drafted Reply" so coordinators can resolve issues in seconds.
- **Robust Edge Case Handling:** Gracefully handles sarcasm, mixed feedback, gibberish, and rate-limiting concurrency errors.
- **Full 2-Way Loop:** Automatically sends a friendly auto-reply to the student while simultaneously alerting the coordinator.

## ⚙️ How it works (Node Architecture)
1. **Trigger:** Google Sheets watches for new feedback rows.
2. **Validation:** Filters out empty/gibberish feedback to save AI costs.
3. **Backup:** Preserves original student data before the AI call.
4. **AI Core:** Calls Groq's LLM to extract `sentiment`, `category`, `urgency_score`, and generate a `reply_draft`.
5. **Router:** Splits the data into 4 branches: `Testimonials`, `High Priority Email`, `Action Items`, and `Needs Review`.

```mermaid
flowchart LR
    A[Google Sheets Trigger] --> B[Validation]
    B --> C{Switch}
    C --> D[Backup Data]
    D --> E[Delay 2.5s]
    E --> F[Groq AI API]
    F --> G[Parser]
    G --> H[Code + Router]
    H --> I(Testimonials)
    H --> J(Urgent Email)
    H --> K(Action Items)
    H --> L(Needs Review)
