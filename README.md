# MASAL AI — Real Estate Lead Assistant

MASAL AI helps real estate teams capture enquiries, understand customer needs, prioritize leads, manage follow-ups, chat with an AI sales assistant, and search public property listings.

## Features

- Lead enquiry form with customer name, location, property type, budget, timeline, and message.
- AI-generated lead summary, requirements, concerns, priority, next action, and suggested customer response.
- Lead-specific AI chat with clickable suggested questions.
- Dashboard and analytics for saved leads, priorities, and follow-ups.
- Follow-up reminders that can be marked complete.
- Property search using public web results, with listing links.

## Architecture

The Streamlit interface in `app.py` collects enquiries and displays the dashboard, AI chat, reminders, analytics, and property search. Python functions save and retrieve leads from a local SQLite database named `masalai.db`. The Groq Python client sends lead-analysis and chat requests to Groq. Property search uses Groq's built-in browser search tool. Locally, the API key is read from `.env`; in deployment, it is configured through Streamlit Community Cloud Secrets.

## AI model and API

The app uses Groq's `openai/gpt-oss-120b` model through the Groq Python client and its chat completions API for lead analysis and the lead-specific assistant. The property search feature calls the same model with Groq's browser search tool enabled.

## Run locally

1. Install Python.
2. Open a terminal in this folder.
3. Create and activate a virtual environment:

   ```powershell
   python -m venv .venv
   .\.venv\Scripts\Activate.ps1
   ```

4. Install dependencies:

   ```powershell
   pip install -r requirements.txt
   ```

5. Create a `.env` file in this folder and add your own key:

   ```text
   GROQ_API_KEY=your_groq_api_key
   ```

6. Start the app:

   ```powershell
   streamlit run app.py
   ```


## Technical decisions

- Streamlit was used to build the interactive app in Python.
- SQLite keeps local setup simple and avoids requiring a separate database service.
- Lead analysis is stored with each lead so the AI chat can answer questions using that lead's saved details.
- Completed follow-ups are excluded from active priority counts and the active dashboard ranking.
- Property search shows public listing sources so users can check details with the listing contact.

## Known limitations

- The app requires a valid Groq API key and an internet connection for AI analysis, chat, and property search.
- Public property listings can be outdated or inaccurate; confirm price and availability with the listing contact.
- Local SQLite storage is suitable for a demo, but Streamlit Community Cloud does not guarantee persistence of local files. Use a managed database before relying on this app for durable customer records.
- The app is a prototype and does not include authentication or multi-user access controls.

## Live demo

https://masalai-real-estate-lead-assistant-yiw7dyhomqofxk2tn6maby.streamlit.app/
