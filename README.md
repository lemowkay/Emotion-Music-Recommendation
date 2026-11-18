# 🎵 Emotion-Based Music Recommendation System

A Python and Streamlit project that uses computer vision and a trained neural network to predict an emotion from facial and hand landmarks, then helps users find music on YouTube based on that prediction, a preferred language, and a singer.

> **Project status:** This is a learning and portfolio project. Cloud deployment is being configured; webcam access, dependency compatibility, and opening recommendation links may require additional work.

## ✨ Features

- **Webcam-based detection:** Captures video through `streamlit-webrtc`.
- **Landmark extraction:** Uses MediaPipe Holistic to detect facial and hand landmarks.
- **Emotion classification:** Loads a trained Keras model (`model.h5`) and class labels (`labels.npy`) to predict a class.
- **Live visual feedback:** Displays landmark overlays and the predicted class on the video feed.
- **Music discovery:** Uses the predicted class, language, and singer to construct a YouTube music search.
- **Streamlit interface:** Simple inputs and a recommendation button.

## 🛠️ Technology stack

**Python**, **Streamlit**, **streamlit-webrtc**, **OpenCV**, **MediaPipe**, **TensorFlow / Keras**, **NumPy**, and **YouTube search**.

## 📁 Project structure

```text
Emotion-Music-Recommendation/
├── music.py              # Main Streamlit application
├── inference.py          # Local model inference script
├── data_collection.py    # Collects webcam landmark samples
├── data_training.py      # Trains and saves the neural network
├── model.h5              # Trained classification model
├── labels.npy            # Labels for model predictions
├── emotion.npy           # Locally saved prediction state
├── *.npy                 # Collected training data
├── requirements.txt      # Python dependencies
├── .gitignore
└── README.md
```

## 🚀 Run locally

### 1. Clone the repository

```bash
git clone https://github.com/lemowkay/Emotion-Music-Recommendation.git
cd Emotion-Music-Recommendation
```

### 2. Create and activate a virtual environment

Python **3.11** is recommended for compatibility with the project's older MediaPipe Solutions API.

**Windows PowerShell:**

```powershell
py -3.11 -m venv .venv
.\.venv\Scripts\Activate.ps1
```

**macOS/Linux:**

```bash
python3.11 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

> The code uses `mp.solutions`, so the MediaPipe version must support the legacy Solutions API. If your dependency file uses an incompatible newer MediaPipe release, adjust its version before installing.

### 4. Start the application

```bash
python -m streamlit run music.py
```

Open the local URL shown in the terminal (usually `http://localhost:8501`).

## 🎧 How to use

1. Enter your preferred **language**.
2. Enter a **singer** or artist.
3. Allow the browser to access your camera when prompted.
4. Face the camera so that the model can detect landmarks and predict a class.
5. Select **Recommend me songs** to request a YouTube music search based on the prediction and your preferences.

**Note:** The current code uses Python's `webbrowser.open()` to open YouTube. When hosted on Streamlit Cloud, that runs on the server, not on the visitor's device. Replace it with a browser-facing link such as `st.link_button()` for online deployment.

## 🧠 How it works

```text
Webcam video
     ↓
MediaPipe face & hand landmarks
     ↓
Landmark features
     ↓
Trained Keras model (model.h5)
     ↓
Predicted class (labels.npy)
     ↓
Preferred language + singer
     ↓
YouTube music search
```

## ☁️ Streamlit Community Cloud deployment

1. Push the project to GitHub, including `music.py`, `requirements.txt`, `model.h5`, and `labels.npy`.
2. Visit [Streamlit Community Cloud](https://share.streamlit.io/).
3. Create a new app from this repository and select `music.py` as the main file.
4. Choose a Python version compatible with your TensorFlow and MediaPipe versions (Python 3.11 is a good target for the legacy code).
5. Deploy and review **Manage app → Logs** if a dependency or runtime error occurs.

Live webcam streaming on a hosted app may require WebRTC network configuration, HTTPS camera permissions, and appropriate media-server settings.

## ⚠️ Current limitations

- Emotion predictions are estimates from visual landmarks and should not be treated as reliable assessments of a person's internal emotional state.
- Recommendations currently come from a **YouTube search**, not a dedicated music recommendation API or music-ranking model.
- The app currently writes the prediction to `emotion.npy`. File-based state is not appropriate for separating multiple users in a hosted app; use per-session state instead.
- Cloud deployment may require dependency pinning and changes to the code that opens YouTube links.

## 📌 Repository

[github.com/lemowkay/Emotion-Music-Recommendation](https://github.com/lemowkay/Emotion-Music-Recommendation)
