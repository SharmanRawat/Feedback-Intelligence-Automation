**Feedback Intelligence Automation Engine 🤖⚡**  
   
   
   
 [![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAABmJLR0QA/wD/AP+gvaeTAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAADUlEQVR4nGP4//8/AwAI/AL+p5qgoAAAAABJRU5ErkJggg==)  
](https://github.com/ "https://github.com/")  
An AI-powered n8n workflow that automatically triages event feedback, classifies sentiment and urgency using an LLM, and routes responses to coordinators and students with zero manual sorting.  
**📸 Project Showcase**  
| | |  
|-|-|  
| **Automation Canvas** | **Email Output Example** |   
|    |    |   
   
**🚀 Key Features**  
- **Instant AI Sentiment Analysis:** Classifies feedback into Positive, Negative, Neutral, or Mixed using Groq's Llama 3.3.  
- **Dynamic Urgency Routing:** Assigns a 1-5 urgency score and maps the issue to the correct department (Venue, IT, Speaker, etc.).  
- **Auto-Generated Action Plans:** Creates an immediate "Action Plan" and a "Drafted Reply" so coordinators can resolve issues in seconds.  
- **Robust Edge Case Handling:** Gracefully handles sarcasm, mixed feedback, gibberish, and rate-limiting concurrency errors.  
- **Full 2-Way Loop:** Automatically sends a friendly auto-reply to the student while simultaneously alerting the coordinator.  
**⚙️ How it works (Node Architecture)**  
1. **Trigger:** Google Sheets watches for new feedback rows.  
2. **Validation:** Filters out empty/gibberish feedback to save AI costs.  
3. **Backup:** Preserves original student data before the AI call.  
4. **AI Core:** Calls Groq's LLM to extract sentiment, category, urgency_score, and generate a reply_draft.  
5. **Router:** Splits the data into 4 branches: Testimonials, High Priority Email, Action Items, and Needs Review.  
   
 flowchart LR  
   
 A[Google Sheet Trigger] --> B[Validation]  
   
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
**🔧 How to run this locally (Interactive Demo)**  
Since n8n is an automation tool, you cannot run this live in a browser. However, you can run it locally in **2 minutes**:  
1. **Install n8n:**npm install n8n -g (or run it via Docker).  
2. **Import the workflow:** Download workflow/Feedback_Intelligence_Engine.json and import it into your n8n canvas.  
3. **Swap credentials:** Replace the placeholders YOUR_GROQ_API_KEY, YOUR_GOOGLE_SHEET_ID, and YOUR_GMAIL_AUTH with your own keys.  
4. **Add a dummy row:** Add a test row to your Google Sheet.  
5. **Run it:** Right-click the trigger and hit Execute workflow. Watch the AI send a beautifully formatted email to your inbox instantly.  
**📄 Full Documentation**  
For the complete breakdown (Problem Statement, AI decisions, and final outputs), check out the [**PDF Report**.](docs/SharmanRawat_Scenario3.pdf "docs/SharmanRawat_Scenario3.pdf")  
![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAnEAAAACCAYAAAA3pIp+AAAABmJLR0QA/wD/AP+gvaeTAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAAM0lEQVR4nO3OQQmAUBBAwSeILbyYdDP8jAaxgjcRZhLMNjNntQIA4C/uvTqq6+sJAADvPS2NA0FrXqf/AAAAAElFTkSuQmCC)  
*Built with ❤️ for the n8n Hackathon 2026.*  
