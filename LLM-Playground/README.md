# LLM Inference Playground

> Interactive sandbox to explore inference-time controls (no model retraining).

This small demo shows how to steer a large language model's behavior at inference time using system instructions and sampling controls. It was implemented to demonstrate the difference between "inference tuning" (changing prompts and sampling) and real fine-tuning (retraining model weights).

## Quick start

- Serve the repo root and open the demo in a browser:

```bash
python -m http.server 8000
# then open http://localhost:8000/LLM-Playground/index.html
```

## Main features

- API Key Setup: Uses Google's Gemini API (Generative Language API). Paste your key into the API Key field and click `Validate Key` to list available models. The key is used locally in the browser and not stored by the page.
- Model Selection: After validation the demo displays compatible models and auto-selects a recommended one (prefers `gemini-2.5-flash-lite`, falls back to `gemini-1.5-flash`).
- Presets: Several behavior presets are provided (Innovative, Factual, Kid, PM, No-Nonsense, Custom). Selecting a preset updates system instructions and sampling controls.
- Sampling Controls: Adjust `Temperature`, `Top-P`, `Top-K`, and `Max Output Tokens` to see how sampling affects output.
- System Instructions & User Prompt: A `System Instructions` textarea simulates persona/steering text (hidden prompt). The `User Prompt` is your query. Click `Run Prompt` to generate.
- Output Area: Shows generated text, model used, latency and active sampling settings. If a selected model fails, the demo attempts a safe fallback and shows a notice.

## UI notes & behavior

- Presets modify both sampling values and the hidden system prompt to simulate fine-tuned behaviors without retraining.
- The `Custom` preset is selected automatically when you edit any of the sliders or text areas.
- The demo uses a lightweight `models:list` call for validation and `models/{name}:generateContent` for generation.

## Troubleshooting

- "No compatible models found": ensure your API key has access to the Generative Language API and models that support `generateContent`.
- Authentication errors / quota issues: check the key, billing, and API quota in your Google Cloud console.
- If generation returns an error for a specific model, the demo will try `gemini-1.5-flash` as a fallback.

## Educational notes

- This playground demonstrates inference-time steering (system prompt + sampling) and contrasts it with true fine-tuning, which requires training on many examples to change model weights permanently.

---
Created from the implementation in `index.html`.
