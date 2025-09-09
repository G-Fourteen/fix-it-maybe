# Unity Voice Chat (Windows)

A simple Windows desktop chat app that talks to an AI using **text** and **voice**.

- **Clean neon UI** powered by ttkbootstrap
- Talk by **typing** or **mic**; get replies **as text** and optionally **spoken aloud**
- Downloads the **model list** from Pollinations automatically
- Renders **code blocks** with Copy / Download buttons
- Shows **images** embedded in replies

---

## 1. Requirements (Windows 10/11, Python 3.10+)

Check your Python version:

```bash
python --version
```

Install dependencies:

```bash
pip install -r requirements.txt
```

**Notes:**
- PyAudio (for microphone input) can be tricky on Windows. If `pip install pyaudio` fails, install a wheel (e.g., with `pipwin install pyaudio`) then try again.
- gTTS needs an internet connection to synthesize speech.

## 2. Set Your API Token

Create a file called `.env` in the same folder as the scripts https://auth.pollinations.ai/:


POLLINATIONS_TOKEN=your_token_here


- On launch, the app loads `.env`; if the token is missing, it raises an error and exits.
## 3. Run It

```bash
python windows_voice_chat.py
```

You'll see:
- **Title bar:** Unity Voice Chat
- **Voice Output toggle:** Turn spoken replies on/off
- **Voice dropdown:** Language options (English, Spanish, French, German, Italian, Portuguese, Russian). Limited to these in the app.
- **Model dropdown:** Fetched from Pollinations (/models), default is *unity*
- **Start Talking:** Toggles listening on your default microphone
- **Mute:** Stops current audio playback immediately
- **Send:** Type a message and press Enter or click Send
- **Clear Chat:** Wipes the conversation

If `unity.ico` exists in the folder, it’s used as the app icon.

## 4. How It Works

- Loads your `POLLINATIONS_TOKEN` from `.env`
- Loads `system_instructions.txt`
- Keeps a running message history, sends it to Pollinations API with retries on errors
- Extracts and renders text, code blocks, and `[IMAGE]...[/IMAGE]` tags
- Plays AI replies aloud (if Voice Output is on) by splitting sentences → gTTS → temp MP3 → Windows MCI playback
- Mic input handled by SpeechRecognition + PyAudio

## 5. Troubleshooting

- **“POLLINATIONS_TOKEN not found”** → Add it to `.env` https://auth.pollinations.ai/
- **PyAudio install fails** → Install a prebuilt wheel using `pipwin install pyaudio`
- **Mic errors (invalid device, no transcription, timeout)** → Check Windows microphone privacy permissions and make sure no other app is using the mic
- **No voice output** → Make sure Voice Output is on, gTTS has internet access, and try pressing Mute once to reset
- **Images don’t load** → If the AI gives an image link inside `[IMAGE]...[/IMAGE]`, the app will fetch it; if unreachable, you’ll see an error bubble

## 6. Tech Stack

- **UI:** tkinter + ttkbootstrap (neon theme)
- **ASR:** SpeechRecognition + PyAudio
- **TTS:** gTTS (online) → MP3 → Windows MCI playback
- **API:** Pollinations /openai with retries + /models for available models
- **Extras:** Code block copy/download, optional `unity.ico`, optional `system_instructions.txt`