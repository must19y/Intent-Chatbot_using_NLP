# Intent-Chatbot_using_NLP
!pip install streamlit pyngrok
!wget https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-v3-stable-linux-amd64.tgz
!tar -xvzf ngrok-v3-stable-linux-amd64.tgz

!./ngrok config add-authtoken your_auth_token

import threading
import os
from pyngrok import ngrok

# Clean up ngrok tunnels before starting
ngrok.kill()

# Run Streamlit in the background
def run_streamlit():
    os.system("streamlit run app.py --server.port 8501 --server.address 0.0.0.0")

# Start Streamlit in a separate thread
thread = threading.Thread(target=run_streamlit)
thread.start()

# Connect to ngrok with the correct port
try:
    public_url = ngrok.connect(8501, "http")  # Explicitly specify HTTP tunnel
    print("Streamlit App is Live at:", public_url.public_url)
except Exception as e:
    print("Error connecting to ngrok:", str(e))

