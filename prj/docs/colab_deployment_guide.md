# How to Run Your YouTube Summarizer Project in Google Colab

This guide provides the exact code cells you need to copy and paste into a new **Google Colab** Notebook to run your Streamlit project cloud-based.

## Step 1: Open Google Colab
Go to [Google Colab](https://colab.research.google.com/) and create a **New Notebook**.

## Step 2: Clone Your Repository or Upload Files
Since your code is local, you can zip your project folder (without the `venv` directory) and upload it directly into the Colab file explorer (on the left sidebar). 

*If your code is on GitHub, use this in a cell instead:*
```python
# Create a new code cell and paste this:
!git clone <YOUR_GITHUB_REPO_URL>
%cd <YOUR_REPO_NAME>
```

## Step 3: Install Required Dependencies
Create a new code cell and paste the following to install Streamlit, localtunnel (to generate a public URL), and project dependencies:
```python
# Create a new code cell and paste this:
!pip install streamlit -q
!pip install -r requirements_enhanced.txt -q
!npm install localtunnel -q
```

## Step 4: Fix NLTK and Configure API Key
Create a new code cell. We need to set your Gemini API key and download the necessary NLTK data:

```python
# Create a new code cell and paste this:
import os
import nltk

# 1. Set your Gemini API Key directly in the Colab environment
os.environ["GOOGLE_API_KEY"] = "YOUR_GEMINI_API_KEY_HERE"

# 2. Download crucial NLTK data
nltk.download('punkt')
nltk.download('stopwords')
```

## Step 5: Run the Streamlit App via LocalTunnel
Since Colab doesn't have a native display for Streamlit, we spin up a background server and use `localtunnel` to create a public link you can click to view your app.

```python
# Create a new code cell and paste this:

# Get the IP address needed for the LocalTunnel password
import urllib
print("Password/Enpoint IP for localtunnel is:", urllib.request.urlopen('https://ipv4.icanhazip.com').read().decode('utf8').strip("\n"))

# Run the Streamlit app in the background and expose it to the web
!streamlit run app_enhanced_fixed.py &>/content/logs.txt &
!npx localtunnel --port 8501
```

### 💡 How to use the LocalTunnel Link:
1. When you run **Step 5**, you'll see an IP Address printed (e.g., `34.125.12.XXX`) and a link starting with `https://loca.lt/...`
2. Click the `https://loca.lt/...` link.
3. It will ask for an "Endpoint IP" or password. Paste the IP address that was printed out.
4. Click Submit, and your YouTube Summarizer Streamlit interface will open in your browser!
