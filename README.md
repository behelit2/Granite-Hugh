<img width="2048" height="1536" alt="image" src="https://github.com/user-attachments/assets/1b848e2f-76aa-4dbd-bc4a-d7887fc601c8" />

# Granite-Hugh
HUGH is a terminal-based AI assistant powered by IBM Granite, running locally on your computer. Chat, get coding help, analyze documents and scanned text, and research the web with source citations... all from one simple interface.

🚀 Installation & Setup

Follow these steps to set up and run Hugh.

# FEDORA LINUX

Prerequisites & Dependencies

Before you start, make sure you have the recommended NVIDIA GPU or TPU with 16GB of VRAM. It can be used experimentally with 12GB of VRAM.

Step 1: Install System Packages (Fedora)

Run the following command in your terminal to install the necessary build tools and system dependencies:

sudo dnf install -y python3.12 python3.12-devel gcc gcc-c++ make redhat-rpm-config pkgconf-pkg-config libcurl-devel openssl-devel ca-certificates tesseract tesseract-langpack-eng


Environment Setup

Step 2: Create Virtual Environment & Install Python Packages

Run these commands sequentially in your terminal to set up the Python environment and dependencies:

# Create and activate virtual environment, then upgrade base packaging tools
python3.12 -m venv "$HOME/.venvs/hugh" && source "$HOME/.venvs/hugh/bin/activate" && python -m pip install --upgrade pip setuptools wheel

# Install PyTorch (CUDA 12.8 wheel)
python -m pip install --upgrade torch --index-url https://download.pytorch.org/whl/cu128

# Install required Python packages
python -m pip install --upgrade transformers accelerate bitsandbytes safetensors huggingface_hub sentencepiece protobuf prompt_toolkit ddgs pycurl trafilatura beautifulsoup4 lxml pypdf defusedxml striprtf charset-normalizer Pillow PyMuPDF "lm-format-enforcer==0.11.3"


Model & Configuration Setup

Step 3: Download the Model

Create the target directory and download the model files using Hugging Face CLI:

mkdir -p "$HOME/models/granite-4.2-8b" && hf download ibm-granite/granite-4.2-8b --local-dir "$HOME/models/granite-4.2-8b"


Note: Wait for the download process to complete before proceeding.

Step 4: Add Application Files

Move the following supplied configuration and code files into the model directory ($HOME/models/granite-4.2-8b):

granite.env

hugh_granite.py

Ensure the contents of both files remain unchanged (including the final overrides in granite.env).

Shortcut Setup & Launch

Step 5: Create Launcher Script

Create a helper shell script in your home directory to easily launch the application:

cat << 'EOF' > ~/hugh.sh
cd "$HOME/models/granite-4.2-8b" && source "$HOME/.venvs/hugh/bin/activate" && source granite.env && python hugh_granite.py
EOF

# Make the script executable
chmod +x ~/hugh.sh


Step 6: Start Hugh

To launch Hugh, run the launcher script from your terminal:

./hugh.sh
