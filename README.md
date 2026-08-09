# Local AI Model Hosting (No-Docker)


## 💻 Hardware Requirements
To run models like Qwen2.5-Coder smoothly, the following specs are highly recommended:
* **RAM:** 16GB (Minimum)
* **VRAM:** 6GB (Dedicated GPU)

---

## ⚙️ Project Overview
This repository provides a step-by-step setup for hosting local LLMs using **Ollama** and **Open-WebUI**. It is specifically designed for:
1. Systems where **Docker** is restricted or not preferred.
2. Users who want to save primary drive space by hosting everything on a **secondary drive (A:)**.

---

## 🚀 Installation & Setup

### 1. Engine Installation (Ollama)
1. Download and run the `OllamaSetup.exe` from [ollama.com](https://ollama.com).
2. **Crucial:** Once installed, right-click the Ollama icon in your system tray and select **Quit**. The settings below will not apply if the engine is running.

### 2. Drive & Environment Configuration
We redirect all heavy data to the **A:** drive to prevent **C:** drive congestion.

1. Search for **"Environment Variables"** in the Windows Start menu.
2. Under **User variables**, create the following two entries:

| Variable Name | Variable Value | Purpose |
| :--- | :--- | :--- |
| `OLLAMA_MODELS` | `A:\ollama_storage` | Redirects LLM weights to A: drive |
| `DATA_DIR` | `A:\webui_data` | Redirects chat history/DB to A: drive |

3. Create the folders manually:
   ```cmd
   mkdir A:\ollama_storage
   mkdir A:\webui_data


## 3. Native Web-UI Setup
We install the interface into a Python virtual environment directly on the secondary drive.
1.Navigate and Initialize:
   cd /d A:
   mkdir local_ai_project
   cd local_ai_project
2.Create and Activate Virtual Environment:
   python -m venv ai_env
   ai_env\Scripts\activate
3.Install Open-WebUI:
   pip install open-webui

##4. Verification & Launch
1.Restart Ollama from your Start menu.
2.Pull the optimized coding model:
   ollama pull qwen2.5-coder
3.Launch the server with network visibility (to access via mobile/other devices):
   open-webui serve --host 0.0.0.0 --port 8080

⚡ Pro-Tip: Automation(For more curious minds)
Instead of typing commands every time, create a launch.bat file in your project folder:
   @echo off
   SET OLLAMA_MODELS=A:\ollama_storage
   SET DATA_DIR=A:\webui_data
   start /b ollama serve
   call A:\local_ai_project\ai_env\Scripts\activate
   open-webui serve --host 0.0.0.0 --port 8080


   📄 Note: You can also find a printable PDF version of this guide in the repository files.
