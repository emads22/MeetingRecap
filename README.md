
# MeetingRecap

## Overview
**MeetingRecap** is a Colab-based application designed to automatically generate detailed meeting minutes from audio recordings. It uses OpenAI's `Whisper` model for high-quality speech-to-text conversion and Meta's `LLaMA` model for summarizing transcripts into well-structured meeting minutes, including key points, takeaways, and action items. The project provides a user-friendly interface built with Gradio, allowing users to quickly upload audio files and retrieve concise meeting summaries.

## Features
- **Speech-to-Text Conversion**: Converts MP3 meeting recordings into text using OpenAI's `Whisper` model.
- **Summarization with Custom Models**: Utilizes the `LLaMA` model for generating clear and organized meeting minutes. Users can choose other models compatible with Hugging Face's `transformers` library.
- **Persistent Model Storage**: Models can be saved in Google Drive for future reuse, or users can choose to store them temporarily in the runtime.
- **Gradio User Interface**: A simple and intuitive UI for uploading audio files and viewing meeting minutes in markdown format.
- **Sample Audio File**: A trimmed sample audio is provided for testing. You can find the sample audio file in the current directory as `trimmed_meeting_audio.mp3`. The original dataset is available [here](https://huggingface.co/datasets/huuuyeah/MeetingBank_Audio/tree/main) if you wish to explore more audio samples. Users can also upload their own MP3 meeting recordings.

## Setup
1. **Clone the repository** and open the Colab notebook.
   - Clone the repository 
     ```bash
     git clone https://github.com/emads22/MeetingRecap.git
     cd MeetingRecap
     ```
   - Open the Colab notebook in Google Colab. You can also find it [here](https://colab.research.google.com/drive/1GfAK-f61cb4Fga8tegghnhkzdyl_krW8).
   - **Select a Runtime**:
    Click on `Runtime` > `Change runtime type`, set the hardware accelerator to `GPU` (preferably `T4` or higher), and connect to the runtime. This ensures faster processing during model inference.
    
2. **Install the required dependencies** by running:
   ```bash
   !pip install -q requests torch bitsandbytes transformers sentencepiece accelerate openai httpx==0.27.2 gradio
   ```
3. **Mount Google Drive** to save models persistently:
   ```python
   from google.colab import drive
   drive.mount("/content/drive")
   ```
4. **Configure secrets** for Hugging Face Hub and OpenAI:
   - Add your Hugging Face Hub token using:
     ```python
     from huggingface_hub import login
     hf_token = userdata.get('HF_TOKEN')
     login(hf_token, add_to_git_credential=True)
     ```
   - Add your OpenAI API key:
     ```python
     from openai import OpenAI
     openai_api_key = userdata.get('OPENAI_API_KEY')
     openai = OpenAI(api_key=openai_api_key)
     ```
5. **Choose where to save the models**:
   - For **persistent storage**, set the directory to Google Drive:
     ```python
     DRIVE_DIR = "/content/drive/MyDrive"
     DRIVE_MODELS_DIR = DRIVE_DIR + "/my_models"
     ```
   - For **temporary storage**, set the directory to the Colab runtime (non-persistent):
     ```python
     DRIVE_DIR = "/content"
     DRIVE_MODELS_DIR = DRIVE_DIR + "/my_models"
     ```
6. **Run the Gradio interface** to start using the app.

## Usage
1. **Uploading Audio**:
   - Use the provided sample audio (trimmed from the [MeetingBank Audio Dataset](https://huggingface.co/datasets/huuuyeah/MeetingBank_Audio/tree/main)) or upload your own MP3 meeting recording.
2. **Processing the Audio**:
   - The app will transcribe the audio using `Whisper`, generate a structured summary using `LLaMA`, and display the output in markdown format.
3. **Output**:
   - The output includes:
     - **Summary**: A concise overview of the meeting.
     - **Key Discussion Points**: Major topics discussed during the meeting.
     - **Takeaways**: Important conclusions or notes.
     - **Action Items**: Tasks with assigned owners.
4. **Saving the Model**:
   - If using Google Drive, models will be saved persistently for faster reuse in future sessions.
   - If using the runtime, models will be deleted after the session ends.

## Sample Audio File
You can use the provided sample audio file `trimmed_meeting_audio.mp3`. Feel free to use your own MP3 audio files as well.

## Contributing
Contributions are welcome! Here are some ways you can contribute to the project:
- Report bugs and issues.
- Suggest new features or improvements.
- Submit pull requests with bug fixes or enhancements.

## Author
- **Emad**  
  [<img src="https://img.shields.io/badge/GitHub-Profile-blue?logo=github" width="150">](https://github.com/emads22)

## License
This project is licensed under the MIT License, which grants permission for free use, modification, distribution, and sublicense of the code, provided that the copyright notice (attributed to [emads22](https://github.com/emads22)) and permission notice are included in all copies or substantial portions of the software. This license is permissive and allows users to utilize the code for both commercial and non-commercial purposes.

Please see the [LICENSE](LICENSE) file for more details.
