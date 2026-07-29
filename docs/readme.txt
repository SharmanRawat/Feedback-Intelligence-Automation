Quick setup for the judges

STEP 1:-  Import the .json file into your n8n.


STEP 2:-  Google Sheet
I've left my test sheet public so you can use it directly:
link ---> https://docs.google.com/spreadsheets/d/1TmjgyEO_xTeTRZthaTeNqlD873GW7ck-ICm_ClcDP_E/edit?usp=sharing
It has the 4 required tabs (Sheet1, Testimonials, Action Items, Needs Review) with all the right column headers.

If you want to use your own sheet instead, just create those exact 4 tabs with the same headers in Row 1.


STEP 3:- Groq API Key
The workflow uses Groq to handle the AI analysis. 
- Grab a free API key from console.groq.com.
- Open the HTTP Request node.
- Replace the Authorization header with: Bearer YOUR_GROQ_KEY


STEP 4:-  Gmail Setup
The workflow uses 4 Gmail nodes to send auto-replies and coordinator alerts. Just open each one and connect your own Gmail account using the n8n credential picker.


STEP 5:-  How to test it
Add a few dummy feedback rows into Sheet1 (positive, negative, mixed, and neutral).
Then in n8n:
- Right-click the Google Sheets Trigger → Execute step
- Click the big orange Execute workflow button

Check your inbox for the emails and check the tabs in Google Sheets. The AI will route everything automatically.

IMPORTANT NOTE:- 
"If the coordinator email arrives empty, it means the Parser node failed to attach the student's original data. To fix this, ensure your Google Sheets columns exactly match the headers in the Parser code (Student Name, Event name, Feedback Test)."

Thank you for your patience. 
