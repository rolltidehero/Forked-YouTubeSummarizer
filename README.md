## YouTube Buddy: Streamline Your YouTube Experience

[Click here to try it out!](https://youtubebuddy.streamlit.app/)

Get information from youtube videos the way you want it.

1. **Video Summary**
2. **Keyword Specific Summary**
3. **Channel Summaries**
4. **Ask question about video via chat**
5. **Create clips**


### Community tokens:
To allow people try out youtubebuddy we allocate open access worth 2.5$ compute costs daily. Once the community tokens are exhausted, users can use their own personal OpenAI access keys.
If you like the app, consider [buying us a coffee](https://buymeacoffee.com/akashe). This would help us cover compute costs.


### Steps to Run the App Locally

Running the app locally involves the following steps:

1. [Set up a Google cloud project in Google workspaces.](https://developers.google.com/workspace/guides/get-started)
2. [Turn on Youtube Data API v3 for your Google project.](https://www.youtube.com/watch?v=fN8WwVQTWYk)
3. [Create OAuth configuration for your project.](https://developers.google.com/workspace/guides/configure-oauth-consent)
4. [Generate access credentials for your Google cloud project.](https://developers.google.com/workspace/guides/create-credentials)
5. [Download 'credentials.json' from your project and keep it locally.](https://techiejackieblogs.com/how-to-create-google-mail-api-credentials-json/)
6. Execute 'streamlit run youtube_summarizer/chatbot.py'.
7. On initial execution, authenticate the project via a Gmail account.
8. This will locally save a 'token.json' file, containing the access token for future access without having to authenticate again.
9. Open the streamlit app in UI and start interacting via chat.


#### Entry points for code
We mostly maintain the codebase for the streamlit entrpoints which allow interacting with YoutubeBuddy via chat. We use Assistants API from OpenAI for the chatbot and use the 'gpt-4o-mini' model for all processing.
- **chatbot.py**: Streamlit UI to get information from youtube using a chatbot.

[Retired entrypoints]
- **process_videos**: Use this entry point to process a single or multiple videos, employing or ignoring keywords.
- **process_channels**: Use this to process single or multiple channels with or without search terms.
- **process_a_playlist**: This entry point processes all the videos in a selected playlist.
- **process_clips**: This entry point creates clips for one or multiple videos.

---
title:
  - Streamlit Fork
author: Heath Brown
created: 2025-01-28 00:28
type: YouTube Summary Tool
tags:
  - YouTube Summary
  - Open-Source Tool
links: 
  - https://github.com/rolltidehero/YouTubesummarizer
  - https://hero-YouTube-summarizer.streamlit.app
  - https://super-duper-robot-699vxrpj6r9f4xg5.github.dev
  - https://YouTubebuddy.streamlit.app/
  - https://docs.streamlit.io/develop/tutorials/databases/supabase
  - https://supabase.io
  - https://YouTubebuddy.streamlit.app
rating: ⭐⭐⭐⭐⭐
---
[hero-YouTube-summarizer.streamlit.app](https://hero-youtube-summarizer.streamlit.app)
# A.I. Setup Instructions & Scripts

Certainly! I'll provide a complete setup guide for using Streamlit and Supabase, focusing on deploying your YouTube summarizer app to Streamlit Community Cloud. I'll include scripts where possible and provide step-by-step instructions.

## Step 1: Set up your local environment

### 1. Clone the repository:
```bash
git clone https://github.com/rolltidehero/YouTubesummarizer.git
cd YouTubesummarizer
```

### 2. Create a virtual environment and activate it:
```bash
python -m venv venv
source venv/bin/activate  # On Windows, use: venv\Scripts\activate
```

### 3. Install the required dependencies:
```bash
pip install streamlit st-supabase-connection
```

## Step 2: Set up Supabase

### 1. Sign up for a Supabase account at [https://supabase.io/](https://supabase.io/)

### 2. Create a new project

### 3. Once your project is created, go to the project settings to find your Project URL and API key

## Step 3: Configure your Streamlit app

### 1. Create a `.streamlit` directory in your project root:
```bash
mkdir .streamlit
```

### 2. Create a `secrets.toml` file in the `.streamlit` directory:
```bash
touch .streamlit/secrets.toml
```

### 3. Add your Supabase credentials to `secrets.toml`:
```toml
[connections.supabase]
SUPABASE_URL = "your_project_url"
SUPABASE_KEY = "your_api_key"
```

## Step 4: Update your Streamlit app

### 1. Open your main Streamlit app file (e.g., `app.py`) and add the Supabase connection:

```python
import streamlit as st
from st_supabase_connection import SupabaseConnection

# Initialize Supabase connection
conn = st.connection("supabase", type=SupabaseConnection)

# Your existing app code here
```

### 2. Use the Supabase connection in your app as needed. For example, to query data:

```python
def get_summaries():
    return conn.query("SELECT * FROM summaries").execute()

summaries = get_summaries()
st.write(summaries)
```

## Step 5: Prepare for deployment

### 1. Create a `requirements.txt` file in your project root:
```bash
pip freeze > requirements.txt
```

### 2. Ensure your `requirements.txt` includes:
```
streamlit
st-supabase-connection
```

### 3. If your app has a different name than `app.py`, create a `streamlit_app.py` file in your project root and import your main app:

```python
from app import main
```

## Step 6: Deploy to Streamlit Community Cloud

### 1. Commit and push your changes to GitHub:
```bash
git add .
git commit -m "Prepare for Streamlit deployment"
git push origin main
```

### 2. Go to [Streamlit Community Cloud](https://share.streamlit.io/)

### 3. Click "New app"

### 4. Select your GitHub repository (rolltidehero/YouTubesummarizer)

### 5. Select the main branch

### 6. Set the main file path to `streamlit_app.py` (or your main app file)

### 7. Set the app URL to `hero-YouTube-summarizer`

### 8. Click "Deploy!"

## Your app should now be deployed and accessible at `https://hero-YouTube-summarizer.streamlit.app`

## Feature suggestions, questions, and tips:

### 1. Consider adding user authentication to protect sensitive summaries.

### 2. Implement a caching mechanism for frequently accessed summaries to improve performance.

### 3. Add a feature to categorize or tag summaries for easier organization.

### 4. Implement a search functionality to find specific summaries quickly.

### 5. Consider adding a feature to export summaries in different formats (e.g., PDF, markdown).

### 6. How can you optimize the summarization process for longer videos?

### 7. Tip: Use Streamlit's `st.cache_data` decorator to cache expensive computations or API calls.

### 8. Question: How will you handle rate limiting from the YouTube API?

### 9. Suggestion: Add a feature to compare summaries of multiple videos side by side.

### 10. Tip: Use Streamlit's `st.progress` to show the progress of long-running summarization tasks.

##  For more detailed information on connecting Streamlit to Supabase, you can refer to the [Streamlit Supabase tutorial](https://docs.streamlit.io/develop/tutorials/databases/supabase).


# Steps to Run the App Locally

## Running the app locally involves the following steps:

## 1. [Set up a Google cloud project in Google workspaces.](https://developers.google.com/workspace/guides/get-started)

## 2. [Turn on YouTube Data API v3 for your Google project.](https://www.YouTube.com/watch?v=fN8WwVQTWYk)

## 3. [Create OAuth configuration for your project.](https://developers.google.com/workspace/guides/configure-oauth-consent)

## 4. [Generate access credentials for your Google cloud project.](https://developers.google.com/workspace/guides/create-credentials)

## 5. [Download 'credentials.json' from your project and keep it locally.](https://techiejackieblogs.com/how-to-create-google-mail-api-credentials-json/)

## 6. Execute 'streamlit run YouTube_summarizer/chatbot.py'.

## 7. On initial execution, authenticate the project via a Gmail account.

## 8. This will locally save a 'token.json' file, containing the access token for future access without having to authenticate again.

## 9. Open the streamlit app in UI and start interacting via chat.


# My GitHub ReadMe.md | YouTube Buddy | Streamline Your YouTube Experience

## [Click here to try it out!](https://YouTubebuddy.streamlit.app/) and get information from YouTube videos the way you want it.

### 1. **Video Summary**

### 2. **Keyword Specific Summary**

### 3. **Channel Summaries**

### 4. **Ask question about video via chat**

### 5. **Create clips**


### Community tokens:
To allow people try out YouTubebuddy we allocate open access worth 2.5$ compute costs daily. Once the community tokens are exhausted, users can use their own personal OpenAI access keys.



# Entry points for code
We mostly maintain the codebase for the streamlit entrpoints which allow interacting with YouTubeBuddy via chat. We use Assistants API from OpenAI for the chatbot and use the 'gpt-4o-mini' model for all processing.
- **chatbot.py**: Streamlit UI to get information from YouTube using a chatbot.

## [Retired entrypoints]
- **process_videos**: Use this entry point to process a single or multiple videos, employing or ignoring keywords.
- **process_channels**: Use this to process single or multiple channels with or without search terms.
- **process_a_playlist**: This entry point processes all the videos in a selected playlist.
- **process_clips**: This entry point creates clips for one or multiple videos.

