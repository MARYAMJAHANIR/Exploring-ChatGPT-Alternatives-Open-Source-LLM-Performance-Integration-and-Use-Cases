# Agent-Based GPT: A Comparative Study of MetaGPT and AutoGen

This repository contains the findings and methodology for the research paper:  
**[AGENT-BASED GPT: A COMPARATIVE STUDY OF METAGPT AND AUTOGEN]**

---

## 📖 About the Project

This project provides a detailed analysis and comparison of two open-source multi-agent frameworks: **MetaGPT** and **AutoGen**.  
We investigated their capabilities by integrating them with open-source Large Language Models (LLMs) like **CodeLLaMA** and **Mistral**, and compared their performance against larger models like **GPT-4**.  

The study focuses on:  
- Software requirements and installation procedures  
- Output consistency across frameworks  
- Practical use cases such as automated game generation  

The main goal was to determine whether open-source models provide a **viable alternative** to expensive, proprietary AI models for complex tasks.  

---

### ✨ Key Findings

* **Performance with Open-Source LLMs**  
  - Both MetaGPT and AutoGen struggled to complete complex code-generation tasks (e.g., creating a Snake game).  
  - Issues included timeout errors, repetitive text instead of code, and memory allocation warnings.  

* **Performance with GPT-4**  
  - With GPT-4 (via Azure OpenAI Service), MetaGPT successfully and consistently generated complete playable games (Snake, 2048, Brick Breaker).  

* **Resource Requirements**  
  - MetaGPT is more resource-intensive, ideally requiring **32 GB of RAM** and a powerful processor for large local models.  
  - AutoGen is lighter but still needs significant resources.  

* **Framework Approach**  
  - **MetaGPT**: Structured meta-programming workflow modeled after human software engineering (with SOPs).  
  - **AutoGen**: Conversation-based multi-agent workflows with customizable agents.  

---

## 🛠️ Environment Setup and Installation

### Hardware & Software Requirements
- **Python**: 3.9 or higher (tested with 3.11.4)  
- **RAM**: 16 GB minimum; 32 GB recommended for large models  
- **Processor**: Strong CPU recommended for MetaGPT  
- **OS**: For Ollama on Windows → WSL required  

---

## Step-by-Step Installation

### 1. Set up virtual environments (recommended) 
# For MetaGPT
conda create -n metagpt python=3.11.4
conda activate metagpt

# For AutoGen
conda create -n autogen python=3.11.4
conda activate autogen

## 🛠️ Installation & Setup

### 1. Install Frameworks
pip install metagpt
pip install pyautogen

### 2. Install and Configure Ollama (for local LLMs like CodeLLaMA/Mistral)
curl https://ollama.ai/install.sh | sh
ollama serve
ollama pull codellama
ollama pull mistral

### 3. Set up LiteLLM Bridge (OpenAI-Compatible API for Local Models)
pip install litellm
pip install async_generator  # if needed

# Start LiteLLM with Ollama
litellm --model ollama/codellama

## ⚙️ Configuration

### MetaGPT Configuration
Edit config.yaml:
OPENAI_API_KEY: "sk-fake-key"
OPENAI_API_BASE: "http://0.0.0.0:8000"

### AutoGen Configuration
Example Python configuration:
import autogen

config_list_codellama = [
    {
        "base_url": "http://0.0.0.0:8000",
        "api_key": "NULL",
        "model": "codellama"
    }
]

coder = autogen.AssistantAgent(
    name="Coder",
    llm_config={"config_list": config_list_codellama}
)

---

## 🚀 Use Cases & Results

This project explored how different AI frameworks and models perform on the task of **end-to-end game generation** from a single prompt.

### 🧪 Open-Source Models (CodeLLaMA / Mistral via Ollama)
- **Prompt**:  
  `"write a CLI snake game based on pygame"`
- **Outcome**: ❌ **Failure**
- **Details**:  
  - Frameworks produced repetitive text outputs (product goals, user stories, competitive analysis) instead of executable code.  
  - Long runtimes with no usable results.  
  - Ollama server encountered **memory allocation errors** even on a 16 GB RAM system.  

### 🔑 GPT-4 (via Azure OpenAI Service)
- **Prompt Examples**:  
  - `"Create a complete 2048 game based on pygame"`  
  - `"Write a brick breaker based on pygame"`  
- **Outcome**: ✅ **Success**
- **Details**:  
  - MetaGPT, configured with GPT-4, generated **full, modular, and playable source code**.  
  - Games included **Snake, 2048, and Brick Breaker**, each runnable directly after code generation.  
  - Output quality was robust, with structured files, comments, and reusable functions.  

### 📊 Key Insight
- Open-source LLMs (CodeLLaMA, Mistral) **struggled with complex multi-step generation** like building playable games.  
- GPT-4 demonstrated **reliable code synthesis and framework orchestration**, producing end-to-end working solutions.

---

## 📄 Full Report

For a complete and detailed overview of the methodology, analysis, and results, please read the full PDF repor!







