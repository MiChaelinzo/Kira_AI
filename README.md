# 🎤 Kira AI VTuber

![Demo of AI VTuber in action](https://github.com/JonathanDunkleberger/Kira_AI/blob/main/VTuber%20Demo%20-%20Kirav3.gif?raw=true)

**Kira** is your personal AI VTuber companion! She chats with you through voice, responds to Twitch chat in real-time, and has her own personality and emotions. Perfect for streamers, content creators, or anyone who wants an AI friend to talk to.

---

## ✨ What Kira Can Do

🎯 **Voice Conversations** - Talk to Kira using your microphone, she'll listen and respond  
💬 **Live Twitch Chat** - Automatically reads and responds to your Twitch chat  
🧠 **Smart Memory** - Remembers your conversations and gets to know you over time  
🎭 **Dynamic Personality** - Changes emotions and personality based on your interactions  
🔊 **Natural Voice** - Speaks with realistic AI-generated voice (Azure/ElevenLabs)

---

## 🚀 Easy Setup Guide

### Step 1: Get the Files
1. **Download this project**
   - Click the green "Code" button above → "Download ZIP"
   - Extract the ZIP file to a folder on your computer
   
   *OR if you use Git:*
   ```
   git clone https://github.com/JonathanDunkleberger/Kira_AI.git
   ```

### Step 2: Install Python
1. **Download Python 3.10 or newer** from [python.org](https://www.python.org/downloads/)
2. **Important**: During installation, check "Add Python to PATH"
3. **Test it works**: Open Command Prompt/Terminal and type `python --version`

### Step 3: Install Required Software

#### Windows Users - IMPORTANT ⚠️
`llama-cpp-python` requires Visual Studio Build Tools and CMake. Install these **FIRST**:

1. **Install Visual Studio Build Tools**
   - Download from [Visual Studio Downloads](https://visualstudio.microsoft.com/downloads/) → "Tools for Visual Studio" → "Build Tools for Visual Studio 2022"
   - During installation, select **"Desktop development with C++"** workload
   - Make sure these components are selected:
     - MSVC v143 - VS 2022 C++ x64/x86 build tools
     - Windows 11/10 SDK
     - CMake tools for Windows

2. **Install CMake** (if not included above)
   - Download from [cmake.org](https://cmake.org/download/)
   - During installation, check "Add CMake to system PATH"

3. **Open a NEW Command Prompt** (to load the new environment variables)

4. **Install llama-cpp-python** (choose one option):
   
   **Option A: CPU-only (easiest)**
   ```
   pip install llama-cpp-python
   ```
   
   **Option B: With NVIDIA CUDA support (recommended for GPU)**
   ```
   set CMAKE_ARGS=-DGGML_CUDA=on
   pip install llama-cpp-python --force-reinstall --no-cache-dir
   ```
   
   **Option C: Use pre-built wheels (fastest)**
   - Download pre-built wheels from [llama-cpp-python releases](https://github.com/abetlen/llama-cpp-python/releases)
   - Or use: `pip install llama-cpp-python --extra-index-url https://abetlen.github.io/llama-cpp-python/whl/cpu`

5. **Install remaining dependencies**:
   ```
   pip install -r requirements.txt
   ```

#### Mac/Linux Users
1. **Open Terminal** in your Kira folder
2. **Run this command**:
   ```
   pip install -r requirements.txt
   ```
   ⏳ *This may take 5-10 minutes - be patient!*

### Step 4: Get Your API Keys (Required)
Kira needs these services to work. **Don't worry - all free tiers/trials!**

📝 **Required Services:**
- **Azure Speech** (for voice) - [Get free key here](https://azure.microsoft.com/en-us/services/cognitive-services/speech-services/)
- **Twitch** (for chat) - [Create app here](https://dev.twitch.tv/console/apps)

🎯 **Optional Services:**
- **ElevenLabs** (other voices) - [Sign up here](https://elevenlabs.io/)
- **Google Search** (web search) - [Get API key here](https://developers.google.com/custom-search/v1/introduction)

### Step 5: Configure Kira
1. **Copy the example file**: Find `.env.example` → copy it → rename copy to `.env`
2. **Open `.env` file** in any text editor (Notepad works!)
3. **Fill in your keys** - paste them after the `=` signs:
   ```
   AZURE_SPEECH_KEY=your_azure_key_here
   AZURE_SPEECH_REGION=your_region_here
   TWITCH_OAUTH_TOKEN=your_twitch_token_here
   ```

### Step 6: Get an AI Model
1. **Download a model file** (these are Kira's "brain"):
   - **Recommended for 8GB+ VRAM**: [Phi-3-mini-4k-instruct-fp16.gguf](https://huggingface.co/microsoft/Phi-3-mini-4k-instruct-gguf) (~7GB) - Best quality
   - **Recommended for 6GB VRAM**: [Phi-3-mini-4k-instruct-q4.gguf](https://huggingface.co/microsoft/Phi-3-mini-4k-instruct-gguf) (~2.4GB) - Good balance
   - **Alternative**: [Llama-3.2-3B-Instruct-Q4_K_M.gguf](https://huggingface.co/bartowski/Llama-3.2-3B-Instruct-GGUF) (~2GB)
   
2. **Put the file** in the `models/` folder in your Kira directory (create it if it doesn't exist)

3. **Update your `.env` file** with the model path:
   ```
   LLM_MODEL_PATH=models/Phi-3-mini-4k-instruct-fp16.gguf
   ```

### Step 7: Start Kira! 🎉
1. **Open Command Prompt/Terminal** in your Kira folder
2. **Run this command**:
   ```
   python bot.py
   ```
3. **Success!** You should see "Kira is now running" and can start talking!

---

## 🛠️ Common Issues & Solutions

**"No module named..."** → Run `pip install -r requirements.txt` again

**"File not found" for model** → Make sure your model file is in the `models/` folder and the name matches your `.env` file

**Kira can't hear you** → Check your microphone permissions and make sure it's not muted

**No Twitch chat** → Verify your Twitch OAuth token and channel name in `.env`

### llama-cpp-python Build Errors (Windows)

**"CMake Error: CMAKE_C_COMPILER not set"** or **"nmake not found"**
→ This means Visual Studio Build Tools is not installed or not properly configured:
1. Install [Visual Studio Build Tools 2022](https://visualstudio.microsoft.com/downloads/) with "Desktop development with C++" workload
2. **Open a NEW terminal** after installation (required to load new PATH)
3. Try installing again: `pip install llama-cpp-python --force-reinstall --no-cache-dir`

**"Building wheel for llama-cpp-python failed"**
→ Try using pre-built wheels instead:
```
pip install llama-cpp-python --extra-index-url https://abetlen.github.io/llama-cpp-python/whl/cpu
```

**For CUDA/GPU support issues:**
```
set CMAKE_ARGS=-DGGML_CUDA=on
set FORCE_CMAKE=1
pip install llama-cpp-python --force-reinstall --no-cache-dir
```

---

## 🔒 Privacy & Safety

✅ **Your data stays private** - All conversations and settings stay on your computer  
✅ **No data is shared** - Kira doesn't send your conversations anywhere  
✅ **API keys are secure** - Keep your `.env` file private, never share it online  

---

## 💡 Need Help?

- **Detailed Installation Guide**: See [INSTALLATION.md](INSTALLATION.md) for step-by-step platform-specific instructions
- **Check Issues** tab above for common problems
- **Create a new Issue** if you're stuck
- **Join our community** for tips and tricks

## 📜 License
This project is open source under the MIT License - feel free to modify and share!
