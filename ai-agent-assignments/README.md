# Research Agent Assignments

PaperTrail research-paper assistant and a document-search ReAct notebook.

## Assignment 1: PaperTrail

- [AI Studio project](https://aistudio.google.com/apps/a86d88c2-5d59-4bc6-862d-be6e6cc22273)
- `assignment-1/ai_studio_build_prompt.txt`: app-building prompt.
- `assignment-1/research_agent_prompt.txt`: few-shot system prompt.
- `assignment-1/research_agent_config.json`: portable configuration.
- `assignment-1/ai_studio_live_report.json` and `.txt`: live app exports.

The AI Studio project uses React and Node. This repository also includes a
separate dependency-free local implementation in Python, HTML and JavaScript:

```bash
python assignment-1/server.py
```

Open http://127.0.0.1:8765. Offline mode retrieves matching passages without
calling a model. For live mode, set `GOOGLE_API_KEY` or `GEMINI_API_KEY` in your
server environment before starting. The default model is
`gemini-3.1-flash-lite`; override it with `GEMINI_MODEL` if needed. Live mode
sends the question and retrieved notes to Gemini. Keep keys out of source files.

## Assignment 2: ReAct document-search agent

Open `assignment-2/agent_loop_demo.ipynb` in Colab. Add your Gemini key in Colab
Secrets as `PAPERTRAIL_GOOGLE_API_KEY`, grant this notebook access, and run all
cells. The notebook is self-contained and uses Python standard-library modules.

The agent has a bounded model/action/observation loop with a `search_documents`
tool, an eight-step limit, tool and argument validation, transient-error retries,
and checks that cited source IDs were retrieved. Complete model turns and opaque
thought signatures remain in the model conversation; public traces show tool
actions and observations.

The notebook includes five documents of at least four sentences each and five
questions. Two questions deliberately have no answer in the collection.
`assignment-2/colab_runtime_results.json` contains the exact JSON captured from
the live runtime's export-cell output.

Execution-record provenance: the direct Colab notebook download stalled. The
repository notebook combines the prepared source and captured execution outputs.
The [original executed notebook](https://colab.research.google.com/drive/1EYJl8gAolgLsg-_uE0pUh6Cg-u1CG7E5)
remains in Drive; access follows the owner's sharing settings.

## Validation

```bash
python -m unittest discover -s tests -v
```

All 11 tests passed. All eight notebook code cells executed live in Colab on
2026-10-30. All five questions completed, including correct abstention for two
out-of-corpus topics. The AI Studio app passed offline retrieval, no-match
abstention, and a live Gemini request with a cited answer. Initial requests to
`gemini-3.8-flash` returned HTTP 503; `gemini-3.1-flash-lite` succeeded.

Samples are fictional teaching notes. Citation-ID validation does not prove
semantic support for every claim; check the underlying passages. The model ID
and quota available to an account may vary.

## Source credits

The notebook adapts the course [agent loop starter](https://github.com/aditi-govindu/gemini-recipe-agent/blob/main/agent_loop_demo.ipynb)
and [recipe-agent example](https://github.com/aditi-govindu/gemini-recipe-agent/blob/main/recipe_agent_gemini.ipynb).
API references: [generateContent](https://ai.google.dev/api/generate-content),
[function calling](https://ai.google.dev/gemini-api/docs/function-calling),
[thinking/signatures](https://ai.google.dev/gemini-api/docs/thinking), and the
[model catalog](https://ai.google.dev/gemini-api/docs/models).
