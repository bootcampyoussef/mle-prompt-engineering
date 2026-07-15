# Prompt Engineering

A notebook-based learning path for prompt engineering with real provider calls. The notebooks use the OpenAI Python library with [Groq](https://console.groq.com/docs) as the primary provider and [Mistral](https://docs.mistral.ai/) as the alternative. The concepts build progressively from prompt anatomy to structured outputs, ReAct-style tool use, guardrails, and prompt evaluation.

## Learning Objectives

By the end of this repository, you should be able to:

- Write zero-shot and few-shot prompts that reliably produce structured outputs.
- Design prompts for multi-step reasoning with concise, inspectable final
  outputs.
- Implement a ReAct-style workflow for tasks requiring external information.
- Extract structured data from unstructured text using schema-oriented prompt
  design and validation.
- Design guardrails that constrain LLM outputs to safe, on-topic responses,
  including content filtering, prompt-injection resistance, and PII detection.

## Learning Path

| File / Folder | Description |
|---|---|
| [**01 - Prompting Foundations**](01-prompting-foundations.ipynb) | Build prompt contracts, run zero-shot and few-shot prompts, and compare real provider responses. |
| [**02 - Structured Outputs**](02-structured-outputs.ipynb) | Use JSON-oriented prompting and Pydantic validation to turn model text into trustworthy data. |
| [**03 - Multi-Step Reasoning and ReAct**](03-multi-step-reasoning-and-react.ipynb) | Build an inspectable reason-act-observe loop with local tools and provider calls. |
| [**04 - Guardrails and Safety**](04-guardrails-and-safety.ipynb) | Add pre-call and post-call checks for prompt injection, PII-like input, off-topic requests, and unsafe outputs. |
| [**05 - Prompt Evaluation Mini-Project**](05-prompt-evaluation-mini-project.ipynb) | Evaluate candidate prompts against a small labeled dataset and write an evidence-based improvement report. |

### Additional Folders and Files

| File / Folder | Description |
|---|---|
| [**assets**](assets/) | Visual aids referenced in the notebooks. |
| [**.env.example**](.env.example) | Provider configuration template. |
| [**pyproject.toml**](pyproject.toml) | Project configuration and dependencies. |
| [**uv.lock**](uv.lock) | Dependency lock file. |

## Setup

> [!NOTE]
> Throughout these steps, text in angle brackets like `<repo-name>` is a
  **placeholder**. Replace it including the `< >` brackets with your own
  value. For example, `cd <repo-name>` becomes `cd mle-prompt-engineering`.

### 1. Create the Repository from the Template

Click **Use this template** on GitHub.

When creating the repository:

- Set yourself as the **Owner**
- Choose a repository name
- Disable **Include all branches**
- Click **Create repository**

> [!IMPORTANT]
> If you are working in pairs or groups, only **one person** should complete this step.

---

### 2. Add Collaborators (Pairs/Groups Only)

If working with teammates:

1. Open the repository on GitHub
2. Go to **Settings → Collaborators**
3. Add your teammates as collaborators
4. Share the repository link with your team

Teammates should accept the invitation before continuing.

---

### 3. Clone the Repository

Copy the SSH URL from the **Code** button on GitHub, then run:

```bash
git clone <copied-ssh-url>
```

The copied SSH URL will look like `git@github.com:<your-username>/<repo-name>.git`.

---

### 4. Move into the Project Folder and Install Dependencies

This installs all dependencies and creates a virtual environment in `.venv/`.

```bash
cd <repo-name>
uv sync
```

---

### 5. Set Up Environment Variables

Copy the example file and fill in your API keys:

```bash
cp .env.example .env
```

Open `.env` and set `LLM_PROVIDER` to `groq` or `mistral`, then add the matching key:

- **Groq (primary):** Create a key at [console.groq.com/keys](https://console.groq.com/keys) and set `GROQ_API_KEY`.
- **Mistral (alternative):** Create a key at [console.mistral.ai/api-keys](https://console.mistral.ai/api-keys) and set `MISTRAL_API_KEY`.

The notebooks run in dry-run mode without a key, but real provider calls require one.

> [!CAUTION]
> Never commit `.env` to version control. It contains your personal API keys.

---

### 6. Open the Notebooks

> [!NOTE]
> Make sure you open VS Code from the project root so it automatically detects the environment created by `uv sync`.

Launch VS Code in the project root folder:

```bash
code .
```

Then open a notebook and select the Python environment created by `uv sync` as the kernel.

## API Usage Notes

- Provider free tiers, rate limits, model names, and billing rules can change.
  Check the provider console before running large evaluations.
- The mini-project reads `MAX_EVAL_CASES` from `.env` so you can limit token use
  while testing.
- The notebooks use OpenAI-compatible chat completions through configurable
  `base_url` values rather than provider-specific SDKs.

## Professional Tooling Context

The notebooks use direct provider calls so the mechanics stay visible. In
production, the same patterns often map to provider and framework features:

- [JSON mode and structured outputs](https://console.groq.com/docs/structured-outputs)
  and [function calling](https://docs.mistral.ai/capabilities/function_calling)
  for schema-constrained responses.
- [LangChain](https://docs.langchain.com/oss/python/langchain/overview) and
  [PydanticAI](https://ai.pydantic.dev/) are examples of frameworks for tool
  routing and orchestration.
- Guardrail services or policy engines for safety checks.
- Evaluation tools such as [Promptfoo](https://www.promptfoo.dev/docs/intro/)
  and [LangSmith](https://docs.smith.langchain.com/evaluation) support
  regression testing and observability.
