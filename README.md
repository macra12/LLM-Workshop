# LLM Fundamentals

Hands-on notebooks for prompting, RAG, tool calling, agents, and Khmer/Lao OCR fine-tuning.

## Project structure

```text
llm-fundamentals-tp2/
├── notebooks/
│   ├── session-1/                 # LLM basics, RAG, tools, and agents
│   └── session-2/                 # Ollama prompting and OCR fine-tuning
├── scripts/                       # Windows launchers and model downloader
├── slides/                        # Course PDFs
├── artifacts/                     # Generated OCR adapters (created when needed)
├── requirements.txt
└── README.md
```

Generated folders such as `.venv`, caches, compiled files, and `artifacts` are ignored by Git.

## 1. Install the regular environment

The project uses Python 3.11.9:

```powershell
"C:\Program Files\Python311\python.exe" -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

Ollama must also be installed. The prompting exercises use:

```powershell
ollama pull gemma4:e2b
```

## 2. Session 1 notebooks

Start Jupyter inside the Session 1 folder so its helper modules import correctly:

```powershell
cd notebooks\session-1
..\..\.venv\Scripts\python.exe -m jupyter lab
```

Run the notebooks in order:

1. `01_llm_basics.ipynb`
2. `02_rag.ipynb`
3. `03_tool_calling_and_mcp.ipynb`
4. `04_ai_agents.ipynb`

Notebooks 2–4 support Ollama, Gemini, or another OpenAI-compatible API through `llm_client.py`.

## 3. Ollama prompting

From the project root, run:

```powershell
.\.venv\Scripts\python.exe -m jupyter lab notebooks\session-2\01_ollama_prompting.ipynb
```

Select the regular project `.venv` kernel.

## 4. Khmer/Lao OCR fine-tuning

OCR uses the separate CUDA environment `.venv-unsloth`. Start it with one command:

```powershell
# Khmer (default)
.\scripts\start_ocr.cmd

# Lao
.\scripts\start_ocr.cmd -Language lao
```

The launcher checks CUDA, the RTX GPU, Unsloth, and the Gemma 4 model before opening the notebook. The completed 7.60 GB model is stored at:

```text
D:\models\gemma-4-E2B-it-unsloth-bnb-4bit
```

If the model ever needs to be downloaded again, run:

```powershell
.\scripts\download_gemma4_model.cmd
```

Fine-tuned adapters are saved under `artifacts/`. The default 60-step run is a small test suitable for the laptop's 8 GB RTX 4060 GPU.

## Slides

- `slides/llm_fundamentals.pdf`
- `slides/tp2_special_lecture_ii.pdf`

## Safety note

`notebooks/session-1/simple_mcp.py` includes a learning tool that can write files. Run it only against files you intend to modify.
