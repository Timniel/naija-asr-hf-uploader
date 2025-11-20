
# Naija ASR Hugging Face Uploader

This repository contains a Python automation script designed to package processed audio data and transcripts into a Hugging Face `Dataset` object and push it directly to the Hub.

It is specifically configured to publish the **Naija-ASR-Corpus v1.0 (NAC-v1.0)**, mapping local audio files to a transcript CSV/Excel file.

## 🚀 Features

*   **Google Drive Integration**: Mounts and reads data directly from cloud storage.
*   **Path Mapping**: Automatically matches transcript row indices to filename patterns (e.g., Row 1 -> `pidgin_0001.wav`).
*   **Validation**: Checks if all audio files referenced in the transcript actually exist before processing.
*   **Audio Casting**: Converts file paths into Hugging Face `Audio` features (resampled to 16kHz).
*   **Automated Documentation**: Generates and uploads a formatted `README.md` (Model Card) with YAML metadata directly to the Hub.

## 📋 Prerequisites

To run this script, you need:

1.  **Hugging Face Account**: You need a [Write Token](https://huggingface.co/settings/tokens).
2.  **Processed Data**:
    *   A folder of `.wav` clips (e.g., `clips/`).
    *   A transcript file (`.csv` or `.xlsx`) where the first column contains text.
3.  **Environment**: Google Colab (recommended) or a local Python environment with `ffmpeg` installed.

## 🛠️ Installation & Setup

### 1. Dependencies
The script installs the necessary libraries automatically, but if running locally:

```bash
pip install datasets huggingface_hub librosa soundfile pandas openpyxl
```

### 2. Configuration
Open `main.py` (or your notebook) and update the **Configuration Section** at the top:

```python
# Path to folder containing 'pidgin_0001.wav'
AUDIO_FOLDER_PATH = "/content/drive/MyDrive/clips"

# Path to your Excel or CSV file
TRANSCRIPT_FILE_PATH = "/content/drive/MyDrive/transcripts.xlsx"

# Your Hugging Face Repo ID (Must create this empty repo first or allow script to create it)
REPO_ID = "your-username/Pidgin_ASR_Dataset"
```

## 🏃 Usage

1.  **Run the script**:
    ```python
    python process_data.py
    ```
2.  **Authenticate**: The script will prompt you to login to Hugging Face. Paste your **Write Token**.
3.  **Verify**: The script will validate file paths.
4.  **Upload**: The dataset will be pushed to the specified `REPO_ID`.

## 📂 Dataset Structure on Hub

Once uploaded, the dataset on Hugging Face will have the following columns:

*   `audio`: An audio array containing the sampled data and sampling rate (16kHz).
*   `text`: The transcription string.

## 📜 License Logic

The script automatically appends a `README.md` to the Hugging Face repository specifying that the data is derived from the **Universal Dependencies Naija Spoken Corpus (UD_Naija-NSC)** and is licensed under **CC-BY-SA 4.0**.

## 👥 Credits

*   **Script Author:** NAC Team
*   **Data Source:** UD_Naija-NSC
