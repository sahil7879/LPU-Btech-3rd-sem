# Activity 03: Build a Local LLM Chat Application with Ollama and LangChain

## Activity format

- Individual activity
- Beginner level
- No paid API or cloud account required
- No prior LangChain experience required
- Recommended duration: 90–120 minutes
- Primary operating system: Windows 10 or Windows 11

## What you will build

You will build a terminal-based chat application that runs a small language model on your own computer.

The application will support:

- multi-turn conversation;
- a system instruction;
- streamed model output;
- adjustable temperature;
- adjustable top-p;
- an optional random seed;
- conversation-history reset;
- zero-shot, one-shot and few-shot prompting;
- role, context, constraint and structured-output prompting;
- prompt chaining and response revision.

The application uses:

- **Python** for the program;
- **Ollama** to download and run the local model;
- **LangChain** to represent chat messages and connect Python to Ollama;
- **Gemma 3 1B** as the default local model.

---

# 1. Why use a local language model?

Most public AI chat applications run models on remote servers. Your prompt travels from the client application to a hosted service, the service performs inference, and the answer returns to the client.

Ollama allows supported models to run locally. After the model has been downloaded, this activity can generate responses without calling a paid model API.

## What local execution helps us observe

### Model and application are different components

The model generates text. The Python program manages the user interface, conversation history, settings and error handling. Ollama loads and serves the model. LangChain connects the program to the model service.

### Training and inference are different

You will not train Gemma 3 during this activity. The downloaded model already contains learned parameters. Your computer performs **inference**, which means it uses those parameters to generate an answer for a new input.

### Chat history is supplied as context

The model does not maintain your Python program's conversation automatically. The application stores earlier messages and sends the relevant history again with the next request.

### Generation is probabilistic

At each generation step, the model assigns probabilities to possible next tokens. Temperature and top-p influence how the application samples from those possibilities.

### Smaller models involve trade-offs

A small model is easier to run on limited hardware, but it may follow complex instructions less reliably, know fewer facts and make more mistakes than a larger model. This makes it useful for learning because its strengths and limitations are easier to observe.

## Real-world use-case scenarios

Local models may be considered for:

- offline drafting where internet access is unreliable;
- private experimentation with non-sensitive sample data;
- prototypes that should not incur an API charge for every request;
- classroom demonstrations of inference and sampling;
- local document classification or summarization;
- low-latency assistance on a workstation or edge device;
- testing an application before selecting a hosted production model.

A local model does not automatically make an application secure or responsible. Developers must still consider access controls, logs, model licensing, harmful output, prompt injection, data retention and user oversight.

---

# 2. What is LangChain?

## Plain-language definition

LangChain is an open-source application framework for working with language models. It provides standard Python interfaces for models, messages, prompts, tools, retrieval, structured output and agent workflows.

LangChain does not contain the language model used in this activity. Gemma 3 is the model, Ollama runs the model, and LangChain connects the Python application to Ollama.

## What LangChain is not

LangChain is not:

- an LLM;
- a replacement for Ollama;
- a model-training system in this activity;
- a graphical chat interface;
- a source of factual knowledge;
- a guarantee that a model response is correct or safe.

LangChain organizes application components. The selected model still determines the basic language capability, and the application developer remains responsible for evaluation and safeguards.

## Why use LangChain in this activity?

It would be possible to call Ollama's local HTTP API directly from Python. LangChain is used here because it demonstrates abstractions that also appear in larger LLM applications.

### Standard model interface

`ChatOllama` provides methods such as `invoke()` and `stream()`. An application can use similar LangChain interfaces with other supported model providers, although provider features and parameters still differ.

### Standard message types

LangChain represents conversation context using message objects:

- `SystemMessage` contains application instructions;
- `HumanMessage` contains user input;
- `AIMessage` contains a model response.

These roles make it easier to build and inspect a multi-turn conversation.

### Streaming

LangChain can return output token by token or chunk by chunk. The student sees the response appearing progressively in the terminal.

### Composition

More advanced applications can connect a model to prompt templates, document retrievers, structured-output schemas, tools and multi-step workflows.

### Easier model experiments

The same Python application structure can be reused while changing the local model or generation settings. This helps compare models without rebuilding the whole application.

## How the components work together

```text
Student
   |
   v
Python terminal interface
   |
   |  HumanMessage + previous messages
   v
LangChain ChatOllama
   |
   |  Local request to localhost:11434
   v
Ollama model server
   |
   v
Gemma 3 1B performs inference
   |
   |  Generated response chunks
   v
LangChain streaming interface
   |
   v
Python displays the answer and saves it in chat history
```

## LangChain components used in this activity

| Component | Purpose |
|---|---|
| `ChatOllama` | Connects LangChain to the local Ollama chat model |
| `SystemMessage` | Stores the persistent assistant instruction |
| `HumanMessage` | Represents each student message |
| `AIMessage` | Stores the completed model response in history |
| `model.stream()` | Returns the response progressively |
| Message list | Supplies short-term conversational context |

The message list in this beginner application exists only in memory while the Python process is running. Closing the program removes the history because the activity does not connect a database or persistent memory store.

## Real-world LangChain use cases

### Document question answering and RAG

A document assistant can retrieve relevant sections from policies, manuals or product documentation and place those sections in the model context before requesting an answer.

Example: an employee asks about a leave policy, and the application retrieves the approved policy paragraphs before the model responds.

### Customer-support assistance

An application can combine conversation messages, customer-provided information, approved knowledge and a structured response format.

Example: the model summarizes a support request and produces fields that a ticketing system can read.

### Information extraction

Structured output can convert free-form text into predictable fields such as category, date, product and requested action.

Example: an email-processing application extracts an issue type and urgency for staff review.

### Tool-enabled assistants

LangChain tools can connect a model-driven application to functions that search a database, call an API, perform a calculation or retrieve current information.

Example: a service assistant calls an approved order-status function instead of guessing whether an order has shipped.

### Agent workflows

An agent combines a model with tools and an execution loop. The model can select a tool, inspect the result and continue until it returns a final answer or reaches a stop condition.

Example: a research assistant retrieves documents, extracts relevant facts and prepares a cited summary.

This activity does not create an agent. It uses `ChatOllama` as a standalone chat model so students can understand the model call, messages and sampling controls before adding tool-selection loops.

### Conversation state

Applications can maintain short-term message history for a conversation and, when properly designed, store selected information across sessions.

Example: a tutoring application remembers the current lesson and the student's previous question during one learning session.

### Model comparison and migration

A development team can place multiple supported models behind similar application interfaces and evaluate them on the same test cases.

Example: a team compares a small local model with a hosted model for latency, output quality and cost before selecting a production design.

## When LangChain may be unnecessary

For a single model request, a direct Ollama client or HTTP call may be simpler. LangChain becomes more useful when the application needs consistent message handling, streaming, model substitution, retrieval, structured output, tools or multi-step orchestration.

Using a framework adds dependencies and abstractions. Developers should use only the components that provide a clear benefit to the application.

---

# 3. Model selection

## Default model: `gemma3:1b`

This activity uses:

```text
gemma3:1b
```

The Ollama model library lists this as a 1-billion-parameter, text-input model with an approximately 815 MB model package and a 32K context window.

It is selected because it is:

- small enough for introductory local experiments;
- instruction-tuned for chat-style tasks;
- capable of simple classification, summarization and rewriting;
- large enough to demonstrate zero-shot and few-shot prompting more reliably than extremely small models.

## Smaller fallback: `qwen3:0.6b`

If the default model is too slow or cannot load on the available computer, use:

```text
qwen3:0.6b
```

Ollama lists this quantized model at approximately 523 MB. It is smaller, but its answers may be less consistent. It may also use a reasoning mode depending on the current Ollama and integration versions.

Do not use `qwen3-embedding:0.6b` for this activity. An embedding model creates numerical representations for retrieval and similarity tasks; it is not the conversational generation model required by this chat application.

---

# 4. Prerequisites

You need:

- Windows 10 22H2 or newer;
- a supported 64-bit computer;
- sufficient free storage for Ollama, Python packages and the selected model;
- Python 3.10 or newer;
- internet access during installation and model download;
- a terminal such as Command Prompt, PowerShell or Windows Terminal.

A dedicated GPU is not required for understanding the activity. CPU generation may be slower.

---

# 5. Install and verify Ollama

## Step 1: Install Ollama

Download Ollama for Windows from:

<https://ollama.com/download/windows>

Run the installer. Ollama normally starts in the background after installation and serves its local API at `http://localhost:11434`.

## Step 2: Open a new terminal

Close any terminal that was already open before the installation. Open Command Prompt or PowerShell again so it can find the new `ollama` command.

## Step 3: Verify the installation

```cmd
ollama --version
```

If a version number appears, the command is available.

## Step 4: Download the model

```cmd
ollama pull gemma3:1b
```

The download occurs once. Ollama keeps the model locally for later use.

## Step 5: Confirm that the model is installed

```cmd
ollama list
```

You should see `gemma3:1b` in the output.

## Step 6: Test the model directly

```cmd
ollama run gemma3:1b
```

At the Ollama prompt, enter:

```text
Explain a token in one simple sentence.
```

Enter `/bye` to leave the Ollama chat.

This direct test separates an Ollama problem from a later Python or LangChain problem.

---

# 6. Create the Python environment

## Step 1: Create a project folder

```cmd
mkdir local-llm-chat
cd local-llm-chat
```

## Step 2: Create a virtual environment

```cmd
py -m venv .venv
```

A virtual environment keeps the activity's Python packages separate from other projects.

## Step 3: Activate the environment

### Command Prompt

```cmd
.venv\Scripts\activate.bat
```

### PowerShell

```powershell
.\.venv\Scripts\Activate.ps1
```

If PowerShell blocks activation, use Command Prompt and the `.bat` command instead.

## Step 4: Upgrade pip

```cmd
python -m pip install --upgrade pip
```

## Step 5: Install LangChain's Ollama integration

```cmd
python -m pip install --upgrade langchain langchain-ollama
```

The `langchain-ollama` package provides the `ChatOllama` class used by the application.

---

# 7. Understand the application before writing it

The program contains five main parts.

## Part A: Model configuration

`ChatOllama` identifies the local model and sends generation settings to Ollama.

```python
ChatOllama(
    model="gemma3:1b",
    temperature=0.2,
    top_p=0.9,
)
```

## Part B: System message

A system message establishes the assistant's general role and boundaries.

```python
SystemMessage(content="You are a concise learning assistant.")
```

The system message influences behaviour, but a small model may not follow every instruction perfectly.

## Part C: Conversation history

The application stores system, human and AI messages in a Python list.

```python
history = [SystemMessage(...), HumanMessage(...), AIMessage(...)]
```

Each new request sends this list to the model. Longer histories consume more context tokens and require more processing.

## Part D: Streaming

Streaming displays generated text as it arrives instead of waiting for the complete answer.

```python
for chunk in model.stream(history):
    print(chunk.content, end="")
```

## Part E: Local commands

Commands beginning with `/` change the Python application's state instead of being sent to the model.

Examples:

```text
/temperature 0.7
/top_p 0.9
/clear
/settings
/exit
```

---

# 8. Build the chat application

Create a file named:

```text
chat_app.py
```

Paste the following code into it.

```python
from __future__ import annotations

from langchain_core.messages import AIMessage, HumanMessage, SystemMessage
from langchain_ollama import ChatOllama


MODEL_NAME = "gemma3:1b"
DEFAULT_SYSTEM = (
    "You are a concise learning assistant for first-year students. "
    "Explain technical ideas in plain language. "
    "If information is uncertain or missing, say so instead of inventing facts."
)

settings = {
    "temperature": 0.2,
    "top_p": 0.9,
    "seed": None,
}

system_instruction = DEFAULT_SYSTEM
history = [SystemMessage(content=system_instruction)]


def build_model() -> ChatOllama:
    """Create a LangChain chat model using the current settings."""
    return ChatOllama(
        model=MODEL_NAME,
        temperature=settings["temperature"],
        top_p=settings["top_p"],
        seed=settings["seed"],
        num_ctx=4096,
        num_predict=300,
        validate_model_on_init=True,
    )


def display_settings() -> None:
    print("\nCurrent settings")
    print(f"  model       : {MODEL_NAME}")
    print(f"  temperature : {settings['temperature']}")
    print(f"  top_p       : {settings['top_p']}")
    print(f"  seed        : {settings['seed']}")
    print(f"  messages    : {len(history) - 1}\n")


def display_help() -> None:
    print(
        """
Commands
  /help                    Show available commands
  /settings                Show model and sampling settings
  /temperature <0.0-1.0>  Change temperature
  /top_p <0.05-1.0>       Change nucleus-sampling threshold
  /seed <integer|none>     Set a repeatable seed or remove it
  /system <instruction>    Replace the system instruction and clear history
  /clear                   Clear chat history but keep the system instruction
  /exit                    Close the application
"""
    )


def reset_history() -> None:
    history.clear()
    history.append(SystemMessage(content=system_instruction))


def content_as_text(content) -> str:
    """Convert either string content or content blocks into printable text."""
    if isinstance(content, str):
        return content
    if isinstance(content, list):
        pieces = []
        for block in content:
            if isinstance(block, dict):
                pieces.append(str(block.get("text", "")))
            else:
                pieces.append(str(block))
        return "".join(pieces)
    return str(content)


def handle_command(command: str) -> tuple[bool, bool]:
    """Return (command_was_handled, rebuild_model)."""
    global system_instruction

    parts = command.strip().split(maxsplit=1)
    name = parts[0].lower()
    argument = parts[1].strip() if len(parts) == 2 else ""

    if name == "/help":
        display_help()
        return True, False

    if name == "/settings":
        display_settings()
        return True, False

    if name == "/clear":
        reset_history()
        print("Conversation history cleared.\n")
        return True, False

    if name == "/temperature":
        try:
            value = float(argument)
            if not 0.0 <= value <= 1.0:
                raise ValueError
            settings["temperature"] = value
            print(f"Temperature changed to {value}.\n")
            return True, True
        except ValueError:
            print("Use a temperature from 0.0 to 1.0.\n")
            return True, False

    if name == "/top_p":
        try:
            value = float(argument)
            if not 0.05 <= value <= 1.0:
                raise ValueError
            settings["top_p"] = value
            print(f"Top-p changed to {value}.\n")
            return True, True
        except ValueError:
            print("Use a top-p value from 0.05 to 1.0.\n")
            return True, False

    if name == "/seed":
        if argument.lower() == "none":
            settings["seed"] = None
            print("Random seed removed.\n")
            return True, True
        try:
            settings["seed"] = int(argument)
            print(f"Seed changed to {settings['seed']}.\n")
            return True, True
        except ValueError:
            print("Use an integer seed or /seed none.\n")
            return True, False

    if name == "/system":
        if not argument:
            print("Provide an instruction after /system.\n")
            return True, False
        system_instruction = argument
        reset_history()
        print("System instruction changed and history cleared.\n")
        return True, False

    if name == "/exit":
        print("Chat closed.")
        raise SystemExit

    return False, False


def main() -> None:
    print("Local LLM Chat")
    print(f"Model: {MODEL_NAME}")
    print("Enter /help to see commands. Enter /exit to finish.\n")

    try:
        model = build_model()
    except Exception as error:
        print("Could not connect to Ollama or find the selected model.")
        print("Confirm that Ollama is running and run:")
        print(f"  ollama pull {MODEL_NAME}")
        print(f"Technical message: {error}")
        return

    while True:
        try:
            user_text = input("You: ").strip()
        except (EOFError, KeyboardInterrupt):
            print("\nChat closed.")
            break

        if not user_text:
            continue

        if user_text.startswith("/"):
            handled, rebuild = handle_command(user_text)
            if handled:
                if rebuild:
                    model = build_model()
                continue

        history.append(HumanMessage(content=user_text))
        print("Assistant: ", end="", flush=True)

        complete_answer = ""
        try:
            for chunk in model.stream(history):
                text = content_as_text(chunk.content)
                complete_answer += text
                print(text, end="", flush=True)
            print("\n")
            history.append(AIMessage(content=complete_answer))
        except Exception as error:
            history.pop()
            print("\nThe request failed.")
            print("Check that Ollama is running and the model is installed.")
            print(f"Technical message: {error}\n")


if __name__ == "__main__":
    main()
```

---

# 9. Run and test the application

Make sure the virtual environment is active, and then run:

```cmd
python chat_app.py
```

Enter:

```text
Explain the difference between training and inference using a classroom analogy.
```

Then enter a follow-up without repeating the subject:

```text
Which of those two is happening on my computer right now?
```

If the second response understands “those two,” the application has supplied the earlier messages as context.

Check the settings:

```text
/settings
```

Clear the history:

```text
/clear
```

Now enter the follow-up question again:

```text
Which of those two is happening on my computer right now?
```

The model should now lack the earlier conversational context.

## Observation questions

1. Did the model use earlier messages before `/clear`?
2. What changed after the history was removed?
3. Does Ollama train the model during this conversation?
4. Which application component stores the conversation history?

---

# 10. Temperature experiment

## What temperature means

Temperature changes how strongly generation favours the highest-probability token choices.

- A lower temperature generally produces more focused and repeatable text.
- A higher temperature generally permits more variation.
- Temperature does not measure truth, intelligence or confidence.
- A high temperature cannot add knowledge that the model did not learn or receive as context.

## Experimental rule

Change one setting at a time. Keep the model, prompt and seed the same so the comparison remains meaningful.

## Step 1: Low temperature

Enter:

```text
/clear
/seed 42
/temperature 0.0
/top_p 0.9
```

Then enter:

```text
Write three short names for a campus study-planning assistant. Return names only.
```

Record the response.

## Step 2: Medium temperature

Enter:

```text
/clear
/seed 42
/temperature 0.5
```

Enter the same prompt and record the response.

## Step 3: Higher temperature

Enter:

```text
/clear
/seed 42
/temperature 1.0
```

Enter the same prompt and record the response.

## Observation table

| Temperature | Focus and predictability | Variety | Instruction followed? | Unexpected output? |
|---:|---|---|---|---|
| 0.0 |  |  |  |  |
| 0.5 |  |  |  |  |
| 1.0 |  |  |  |  |

## Questions

1. Which value produced the most predictable response?
2. Which value produced the most variety?
3. Which value would you prefer for factual classification?
4. Which value might be useful for brainstorming?
5. Did higher variation improve correctness?

---

# 11. Top-p experiment

## What top-p means

Top-p is also called nucleus sampling. The model considers a probability-ranked set of next-token candidates whose cumulative probability reaches the selected threshold.

- A lower top-p narrows the candidate set and generally produces more conservative output.
- A higher top-p permits a wider candidate set and generally produces more varied output.
- Temperature changes the probability distribution; top-p limits which portion of that distribution can be sampled.
- Because the controls interact, production applications normally test combinations rather than assuming one universal setting.

## Step 1: Narrow candidate set

```text
/clear
/seed 42
/temperature 0.5
/top_p 0.3
```

Enter:

```text
Suggest three ways a student can organize revision notes. Use one sentence per suggestion.
```

## Step 2: Medium candidate set

```text
/clear
/seed 42
/top_p 0.7
```

Enter the same prompt.

## Step 3: Wider candidate set

```text
/clear
/seed 42
/top_p 1.0
```

Enter the same prompt.

## Observation table

| Top-p | Relevance | Variety | Repetition | Unexpected wording |
|---:|---|---|---|---|
| 0.3 |  |  |  |  |
| 0.7 |  |  |  |  |
| 1.0 |  |  |  |  |

## Questions

1. How did the candidate range affect the responses?
2. Did a wider range always create a better response?
3. Why should temperature remain unchanged during this comparison?
4. Why might classification use more conservative settings than creative writing?

---

# 12. Prompt-engineering methods

Use the following methods individually. Start with `/clear` before each method unless the instructions state otherwise.

## Method 1: Zero-shot prompting

### Meaning

The model receives a task and an input but no worked example.

### Prompt

```text
Classify the following university support message as Technical, Academic, or Administrative. Return the label and one short reason.

Message: “The examination portal shows an error when I upload my form.”
```

### Observe

- Did the model understand the labels without examples?
- Did it follow the requested response format?

### Typical use case

Zero-shot prompting works well for simple tasks the model already understands, such as basic rewriting, summarization or broad classification.

---

## Method 2: One-shot prompting

### Meaning

The prompt supplies one demonstration of the expected relationship between input and output.

### Prompt

```text
Classify a university support message as Technical, Academic, or Administrative.

Example:
Message: “My password reset link has expired.”
Answer: Technical — the problem concerns access to a digital system.

Now classify:
Message: “The examination portal shows an error when I upload my form.”
```

### Observe

- Did the answer imitate the example's format?
- Did one example clarify the meaning of the labels?

### Typical use case

One-shot prompting is helpful when the task is understandable but the required output style is not obvious.

---

## Method 3: Few-shot prompting

### Meaning

The prompt supplies several examples. The examples demonstrate categories, style or decision boundaries.

### Prompt

```text
Classify each university support message as Technical, Academic, or Administrative.

Example 1:
Message: “My password reset link has expired.”
Answer: Technical — access problem involving a digital system.

Example 2:
Message: “Which elective should I select for the data science programme?”
Answer: Academic — question about course selection.

Example 3:
Message: “Where can I collect my identity card?”
Answer: Administrative — question about a university administrative service.

Now classify:
Message: “The examination portal shows an error when I upload my form.”

Return exactly:
Category: <category>
Reason: <one sentence>
```

### Observe

- Did several examples improve category consistency?
- Did the output follow the demonstrated format?
- Could poor examples teach the wrong pattern?

### Typical use case

Few-shot prompting is useful when labels are organization-specific or when the desired style requires demonstrations.

---

## Method 4: Role and system prompting

### Meaning

A role identifies the perspective, audience and boundaries the model should follow. A role does not grant real authority or professional expertise.

### Command

```text
/system You are a beginner-friendly teaching assistant. Explain concepts in plain language, use one everyday analogy, and state when you are uncertain.
```

### Prompt

```text
Explain embeddings to a first-year student.
```

### Observe

- Did the language and detail match the audience?
- Did the role change facts, or mainly change presentation?

### Typical use case

Role prompting can adapt an explanation for students, customers, developers or reviewers while keeping the core task clear.

---

## Method 5: Context-grounded prompting

### Meaning

The prompt supplies the information the model should use. This reduces reliance on unsupported memory, but it does not guarantee that the model will use the context correctly.

### Prompt

```text
Use only the information inside <policy> tags. If the answer is not present, reply “Not stated in the supplied policy.”

<policy>
The fictional campus library is open from 8:00 AM to 8:00 PM on weekdays. It closes at 5:00 PM on Saturday and remains closed on Sunday.
</policy>

Question: What time does the library close on Saturday?
```

Then ask:

```text
Can students enter the library on Sunday during examinations?
```

### Observe

- Did the model use the supplied facts?
- Did it refuse to invent the missing exception?

### Typical use case

Grounded prompts are used in policy assistants, document question answering and retrieval-augmented generation systems.

---

## Method 6: Constraints and structured output

### Meaning

Constraints define boundaries such as length, permitted evidence and prohibited actions. Structured output makes the response easier for software or a reviewer to check.

### Prompt

```text
Summarize the message below.

Constraints:
- Use no more than 35 words.
- Do not invent a policy.
- Do not decide eligibility.
- Mark missing information as “Needs verification.”

Return this structure:
Summary: <text>
Deadline: <text or Needs verification>
Human review: <Yes or No>

Message: “I cannot upload my examination form. Please tell me if the university will accept it late.”
```

### Observe

- Did the model respect the word limit and structure?
- Did it make a decision that the prompt prohibited?

### Typical use case

Structured prompting helps when another program must parse the answer or when reviewers need consistent fields.

---

## Method 7: Task decomposition

### Meaning

Task decomposition separates a complex request into smaller, observable steps. Ask for concise, checkable intermediate results rather than hidden internal reasoning.

### Prompt

```text
Review this fictional support message in four visible steps:

1. Extract only explicitly stated facts.
2. List missing information.
3. Identify possible risks if the request is handled incorrectly.
4. Recommend whether trained staff should review it.

Do not provide private internal reasoning. Provide only the four requested results.

Message: “My exam form is not submitted and today may be the deadline. Please approve it.”
```

### Observe

- Did the smaller steps make the result easier to verify?
- Which step revealed uncertainty?

### Typical use case

Decomposition helps with document review, planning, data extraction and multi-stage workflows.

---

## Method 8: Prompt chaining

### Meaning

Prompt chaining uses the output of one task as the input to another task. Each stage has a separate purpose.

### Chain A: Extract

```text
Extract the problem, stated deadline and requested action from this message. Do not add advice.

Message: “The portal rejects my PDF and the registration deadline is today. Please help me upload it.”
```

### Chain B: Transform

Use the extracted result in the next message:

```text
Using the extracted facts above, write a support ticket summary of no more than 30 words. Do not invent a resolution.
```

### Chain C: Review

```text
Review the summary for omitted facts, unsupported claims and unnecessary personal information. Return Pass or Revise with a one-sentence reason.
```

### Observe

- Did each stage have a clearer responsibility?
- Could an error from the first stage affect later stages?

### Typical use case

Prompt chains are used in extraction, classification, drafting and review workflows. Production chains require validation because early errors can propagate.

---

## Method 9: Critique and revision

### Meaning

The model first produces a draft, then evaluates the draft against explicit criteria and revises it. Self-critique can improve presentation, but it is not an independent guarantee of correctness.

### Draft prompt

```text
Write a short explanation of attention in a Transformer for a first-year student.
```

### Critique prompt

```text
Review your explanation using these criteria:
- technically accurate;
- understandable without advanced mathematics;
- includes one clear example;
- no claim that attention thinks like a person.

List up to three specific improvements.
```

### Revision prompt

```text
Revise the explanation using the improvements. Keep it below 120 words.
```

### Observe

- Did the revision address the listed weaknesses?
- Did the model identify every factual problem?
- Why is external evaluation still needed?

### Typical use case

Critique and revision are useful for drafts, explanations and formatting, especially when the evaluation criteria are explicit.

---

# 13. Compare the prompt methods

Complete the table after running the exercises.

| Method | What information was added? | Main improvement | Remaining limitation | Suitable use case |
|---|---|---|---|---|
| Zero-shot |  |  |  |  |
| One-shot |  |  |  |  |
| Few-shot |  |  |  |  |
| Role/system |  |  |  |  |
| Context-grounded |  |  |  |  |
| Constraints/structure |  |  |  |  |
| Decomposition |  |  |  |  |
| Prompt chaining |  |  |  |  |
| Critique/revision |  |  |  |  |

## Questions

1. Which method produced the most consistent classification?
2. Which method made the output easiest for another program to read?
3. Which method reduced unsupported factual claims?
4. Why can badly chosen few-shot examples make the result worse?
5. Why does a role not turn the model into a qualified professional?
6. Which application would require grounding with approved sources?

---

# 14. Inspect the relationship between the components

Use the completed application to identify each component.

| Component | Role in this activity |
|---|---|
| Gemma 3 1B | Generates tokens using learned parameters |
| Ollama | Downloads, loads and serves the local model |
| LangChain `ChatOllama` | Connects the Python application to Ollama |
| Python loop | Accepts input, handles commands and displays output |
| Message history | Supplies earlier conversation as context |
| System message | Provides persistent role and behaviour instructions |
| Temperature | Adjusts the concentration of token probabilities |
| Top-p | Limits sampling to a cumulative-probability candidate set |
| Seed | Helps reproduce generation when other inputs and settings remain the same |

## Questions

1. Which component contains the trained parameters?
2. Which component stores the current conversation?
3. Which component would you change to build a graphical interface?
4. What would happen if Ollama stopped while Python remained open?
5. Why is this activity inference rather than training?

---

# 15. Optional fallback model

If `gemma3:1b` cannot run acceptably on the available computer:

```cmd
ollama pull qwen3:0.6b
```

Change this line in `chat_app.py`:

```python
MODEL_NAME = "qwen3:0.6b"
```

If reasoning tags appear, add `reasoning=False` inside `ChatOllama(...)`:

```python
return ChatOllama(
    model=MODEL_NAME,
    reasoning=False,
    temperature=settings["temperature"],
    top_p=settings["top_p"],
    seed=settings["seed"],
    num_ctx=4096,
    num_predict=300,
    validate_model_on_init=True,
)
```

Run the same prompt exercises and observe whether the smaller model follows multi-step instructions as consistently.

---

# 16. Troubleshooting

## `ollama` is not recognized

- Close and reopen the terminal after installation.
- Confirm that Ollama is installed.
- Run the command from a new Command Prompt window.

## Python reports that the model does not exist

```cmd
ollama pull gemma3:1b
ollama list
```

## Python cannot connect to Ollama

- Confirm that the Ollama application is running.
- Open a separate terminal and test `ollama run gemma3:1b`.
- If necessary, run `ollama serve` in a separate terminal and leave it open.

## `ModuleNotFoundError: langchain_ollama`

Activate the virtual environment and run:

```cmd
python -m pip install --upgrade langchain langchain-ollama
```

## PowerShell blocks virtual-environment activation

Use Command Prompt:

```cmd
.venv\Scripts\activate.bat
```

## Responses are very slow

- Close memory-intensive applications.
- Keep `num_ctx` and `num_predict` modest.
- Try the `qwen3:0.6b` fallback.
- Remember that CPU-only inference may be slow.

## The model ignores part of a complex prompt

- Shorten the prompt.
- Separate the task into smaller steps.
- Add one or more good examples.
- Request a simple output format.
- Remember that a small model has limited instruction-following capability.

---

# 17. Final individual reflection

Answer the following questions after completing the activity.

1. Why did this activity use a local model instead of a paid API?
2. What is the difference between the model, Ollama, LangChain and the Python application?
3. Where was conversation history stored?
4. How did temperature affect generation?
5. How did top-p affect the candidate token range?
6. Why did the experiment use the same seed while changing sampling controls?
7. What was the difference between zero-shot and few-shot prompting?
8. Which prompt method produced the most reliable output for your task?
9. Why can a well-designed prompt still produce an incorrect answer?
10. When would a larger model or a hosted service be more appropriate?
11. What privacy and security controls would a real local-model application still need?
12. Which tests would you perform before allowing other users to use this chat application?

---

# 18. Main conclusions

- Ollama runs and serves the selected model locally.
- LangChain provides a consistent chat-model interface and message representation.
- Python controls the user experience, settings and history.
- The activity performs inference, not model training.
- Temperature and top-p influence sampling rather than factual knowledge.
- Zero-shot, one-shot and few-shot prompts provide different amounts of demonstration.
- Context, constraints and structured output make the expected behaviour easier to evaluate.
- Prompt chaining separates a larger task into stages, but errors can propagate.
- A small local model is useful for learning and prototypes, but it still needs evaluation and safeguards.

---

# 19. Current official references

- Ollama for Windows: <https://docs.ollama.com/windows>
- Ollama model library, Gemma 3 1B: <https://ollama.com/library/gemma3:1b>
- Ollama model library, Qwen3 0.6B: <https://ollama.com/library/qwen3:0.6b>
- LangChain ChatOllama integration: <https://docs.langchain.com/oss/python/integrations/chat/ollama>
- LangChain ChatOllama reference: <https://reference.langchain.com/python/langchain-ollama/chat_models/ChatOllama>
- LangChain model interfaces: <https://docs.langchain.com/oss/python/langchain/models>
- LangChain messages: <https://docs.langchain.com/oss/python/langchain/messages>
- LangChain tools: <https://docs.langchain.com/oss/python/langchain/tools>
- LangChain agents: <https://docs.langchain.com/oss/python/langchain/agents>
- LangChain memory concepts: <https://docs.langchain.com/oss/python/concepts/memory>
- LangChain structured output: <https://docs.langchain.com/oss/python/langchain/structured-output>
- Ollama Modelfile parameters: <https://docs.ollama.com/modelfile>

Documentation checked: 10 September 2026.
