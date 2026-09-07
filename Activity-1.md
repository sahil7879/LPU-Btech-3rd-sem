# Activity 1: Explore Generative AI and LLMs Through Free Chat Applications

## Overview

In this activity, you will use a free AI chat application to explore the main concepts covered in **CSG202 Unit 1 and Unit 2**. You will compare generative AI with traditional machine learning, investigate common generative-model families, observe how an LLM responds to context and examples, design structured prompts, test an answer for unsupported information, and improve an output through follow-up prompts.

You may use the free version of **ChatGPT**, **Microsoft Copilot**, or **Gemini**. You do not need a Google Cloud account, API key, credit card, paid model, programming environment, or access to Vertex AI.

This is a guided beginner activity. Example prompts and example conversations are provided to help you start. Some challenges intentionally do not provide the answer; use the linked documentation and your observations to complete them.

## Topics covered

### Unit 1 — Foundations of Generative AI

- Artificial intelligence, machine learning, deep learning and generative AI
- Generative AI compared with traditional or discriminative machine learning
- How generative models learn patterns and generate new samples
- GANs, VAEs, diffusion models and Transformer-based models
- Text, image, audio, video and code generation use cases

### Unit 2 — Exploring Large Language Models

- Large Language Models and foundation models
- Tokens, embeddings, Transformers, attention and inference
- Summarization, classification, question answering, translation and conversational use cases
- Zero-shot, one-shot and few-shot prompting
- Structured prompt design and iterative improvement
- Prompt engineering compared with prompt tuning
- Gemini, Google AI Studio, Vertex AI and Model Garden at a conceptual level

## Learning objectives

By the end of the activity, you should be able to:

- identify whether a task requires generation, classification, or both;
- explain the basic relationship among AI, ML, deep learning, generative AI and LLMs;
- match common generative-model families to appropriate use cases;
- describe, at a beginner level, how tokens, embeddings, attention and Transformers contribute to an LLM response;
- construct a prompt with a clear task, context, constraints and output format;
- demonstrate zero-shot and few-shot prompting;
- identify an unsupported claim in an AI-generated response;
- improve an output by naming a specific defect; and
- distinguish a free chat application from Google AI development tools.

## Prerequisites

You need:

- a web browser and internet connection;
- access to any one supported free chat application;
- approximately 90 minutes; and
- a simple text file or notebook in which you can save prompts and observations.

Recommended group size: **two or three students**.

## Important safety rules

- Use only the fictional information supplied in this activity.
- Do not enter real student records, marks, passwords, identity documents, health information, private messages, unpublished university information, or other sensitive data.
- Do not assume that a confident or fluent response is correct.
- Do not ask the chatbot to reveal private internal reasoning. Ask it to provide a short explanation, supporting facts, or a verifiable answer instead.
- Free features, models and usage limits can change. If your selected model becomes unavailable, use the standard free model offered by the application.

## Before starting

1. Open one of the following:
   - [ChatGPT](https://chatgpt.com/)
   - [Microsoft Copilot](https://copilot.cloud.microsoft/)
   - [Gemini](https://gemini.google.com/)
2. Sign in only if the application requires it or you want to preserve your chat history.
3. Start a **new chat**.
4. Record the application name, displayed model name if visible, and the date.
5. Give the chat a recognizable title such as `CSG202 Activity 1` if the application supports chat titles.

> Use a new chat whenever the activity asks for a controlled comparison. Earlier messages become part of the context and can influence later responses.

---

## Part 1 — Meet the chat model

### Step 1.1: Begin with a simple prompt

Enter:

> Explain generative AI to a first-year university student in no more than 80 words. Include one everyday example.

Read the response and identify:

- the task you gave the model;
- the requested audience;
- the length constraint; and
- the example used by the model.

### Step 1.2: Improve an unclear explanation

If the answer contains a term you do not understand, do not begin an unrelated new chat. Ask a focused follow-up such as:

> You used the term “data distribution.” Explain only that term using a classroom analogy and one simple example.

### Example chat

**Student:** What is generative AI?

**AI:** Generative AI is technology that learns patterns from data and creates new content such as text, images or music.

**Student:** Explain “learns patterns” without assuming that I know machine learning. Use an example involving student emails.

**AI:** Imagine reading many student emails and noticing common structures such as a greeting, a question and a closing. A model learns numerical patterns representing such relationships. It can then produce a new email with a similar structure without copying one complete email.

**What this example demonstrates:** The follow-up names the unclear phrase, states the learner's background and provides a relatable context.

### Checkpoint

You should be able to explain why generated content can resemble training examples without necessarily being an exact copy of one example.

---

## Part 2 — AI, ML, deep learning and generative AI

### Step 2.1: Request a hierarchy

Open a new chat and enter:

> Create a beginner-friendly hierarchy showing the relationship among artificial intelligence, machine learning, deep learning and generative AI. For each term, provide a one-sentence definition and one example. If the relationship is not a perfect nested hierarchy, explain the limitation.

### Step 2.2: Test the explanation

Ask the model to classify these tasks:

1. Predict whether an email is spam.
2. Predict tomorrow's temperature as a number.
3. Write a new product description.
4. Create an image from a text description.
5. Summarize a university notice.

Use only these output labels:

- `Traditional predictive ML task`
- `Generative AI task`
- `Could use both`

Ask for a short reason beside every label.

### Step 2.3: Challenge one answer

Select one classification and ask:

> Could a generative LLM perform this task even if the required output is a fixed label? Explain the difference between the model being used and the type of output required.

### Expected observation

A generative model can be prompted to return a category, but the desired task output is still classification. The tool or model family and the task type are related but are not identical concepts.

---

## Part 3 — Compare generative-model families

### Step 3.1: Build a comparison table

Enter the following prompt in a new chat:

> Compare GANs, VAEs, diffusion models and Transformer-based generative models for a beginner. Use a table with the columns `Model family`, `Central idea`, `Common output`, `Example use case`, and `One limitation`. Use no more than 25 words in each cell. After the table, explain in two sentences why these families should not be treated as four versions of the same algorithm.

### Step 3.2: Check the central ideas

Use the documentation links at the end of the activity to verify whether the response contains these important ideas:

- A **GAN** uses a generator and a discriminator that learn through competition.
- A **VAE** learns a structured latent representation and generates by sampling and decoding from that space.
- A **diffusion model** learns to reverse a gradual noising process.
- A **Transformer** uses attention to model relationships in a sequence or across input elements.

If the chatbot contradicts one of these ideas, ask it to revise the affected row and identify the source used for the correction.

### Step 3.3: Use-case challenge

For each case, choose the model family that is most strongly associated with the task and explain your choice. More than one answer can be reasonable, but the reason must refer to the model's strengths.

1. Generate a high-quality image from a text description.
2. Generate and edit realistic faces using adversarial training.
3. Explore smooth variations between learned image representations.
4. Generate a paragraph token by token from a prompt.

### Example follow-up

> You selected a diffusion model for text generation. Is that the most common architecture for modern LLM text generation? Recheck the distinction between an image diffusion model and an autoregressive Transformer.

### Checkpoint

You should be able to give one central idea, one use case and one limitation for each family without claiming that only one family can ever perform a particular task.

---

## Part 4 — Understand an LLM at a conceptual level

This part is a conceptual simulation. A public chat application normally does not expose its exact tokenization, internal embeddings or attention weights.

### Step 4.1: Explore tokens

Enter:

> Explain what a token is in an LLM. Demonstrate with the sentence “Generative AI helps students learn.” Make clear that your token split is only an illustration unless you can access the exact tokenizer used by this chat.

Look for the following idea: a token can be a word, part of a word, punctuation or another text unit. Tokenization converts text into units the model can process.

### Step 4.2: Explore embeddings

Enter:

> Explain embeddings to a beginner using a map analogy. Compare the words “student,” “learner,” “teacher,” and “volcano.” Do not invent exact coordinates. Explain only the relationship.

Expected observation: words or tokens used in related contexts can have representations that are closer in an embedding space. An embedding is a numerical representation, not a dictionary definition stored as ordinary text.

### Step 4.3: Explore attention

Enter:

> In the sentence “The trophy did not fit in the suitcase because it was too large,” what does “it” most likely refer to? Explain briefly how attention can help a Transformer relate important words. Do not claim to show the model's actual hidden attention weights.

Now replace `large` with `small` and ask the question again. Discuss why changing one word can change which earlier word is relevant.

### Step 4.4: Explore next-token generation

Before asking the chatbot, individually predict three plausible continuations for:

> After reading the documentation, the student...

Then enter:

> Give five plausible next short continuations for this incomplete sentence: “After reading the documentation, the student...” Explain why several continuations can be reasonable.

### Step 4.5: Connect the pipeline

Ask:

> Describe this simplified LLM inference flow in six numbered steps: prompt → tokens → embeddings → Transformer attention and layers → next-token probabilities → generated response. Use one sentence per step and state that the real system is more complex.

### Checkpoint

Explain the following in your own words:

- The prompt becomes tokens.
- Tokens are represented numerically.
- Transformer layers use attention and other operations to build contextual representations.
- The model repeatedly selects or samples a next token during inference.
- A likely continuation can still contain an incorrect fact.

---

## Part 5 — Use one source for several LLM tasks

Use the following fictional source throughout Parts 5–8.

### Common source

> The University AI Club will conduct a Generative AI Starter Workshop on 18 September 2026 from 2:00 p.m. to 4:00 p.m. in Lab B-204. It is intended for first-year students and assumes no previous AI or programming experience. The workshop will introduce generative AI, large language models and basic prompt design through short demonstrations. Students should bring a charged laptop and their university identity card. Registration closes at 5:00 p.m. on 16 September 2026. Only 40 seats are available. Registration is completed through the Student Portal under Events. Participation is free. Questions may be sent to the fictional address aiclub@example.edu. The source does not state whether transport, food or certificates will be provided.

### Step 5.1: Summarization

Ask the model to summarize the source in exactly three bullets for a first-year student.

### Step 5.2: Information extraction

Ask the model to extract only the date, time, location, audience, registration deadline, capacity, cost and contact address in a table.

### Step 5.3: Question answering

Ask:

> According to the source, where must a student register and what must the student bring?

### Step 5.4: Classification

Ask the model to label the source as one of: `ACADEMIC EVENT`, `SPORTS EVENT`, `PLACEMENT NOTICE`, or `EXAM NOTICE`.

### Step 5.5: Translation or rewriting

Choose one:

- Translate the announcement into a language understood by your group, while preserving names, dates and the email address.
- Rewrite it in simpler English for a reader unfamiliar with AI.

Afterward, compare the result with the original source and identify any changed or missing fact.

### Discussion

All five tasks use the same LLM, but the requested operation and output format differ. This is why a general foundation model can support many use cases.

---

## Part 6 — Improve a prompt step by step

### Step 6.1: Run a vague baseline

Open a new chat, paste the common source and enter:

> Write an announcement about this.

Save or copy the response as **Run A**.

Check whether the model guessed the audience, length, format or missing information.

### Step 6.2: Learn the prompt structure

Use **R–T–C–C–F–Q** as a checklist:

| Part | Meaning | Question |
|---|---|---|
| R | Role | What useful perspective should the assistant take? |
| T | Task | What exact action should it perform? |
| C | Context | What facts does it need? |
| C | Constraints | What must it include, avoid or limit? |
| F | Format | What should the answer look like? |
| Q | Quality check | How should facts or uncertainty be checked? |

The role is optional. Relevant context and testable instructions are more important than giving the model an impressive job title.

### Step 6.3: Run a structured prompt

Open another new chat and enter:

> **Role:** Act as a university communications assistant.  
> **Task:** Turn the supplied source into a clear announcement for first-year students.  
> **Context:** Use only the information inside the `<source>` tags.  
> **Constraints:** Write 100–120 words. Preserve the exact date, time, room, deadline, seat limit, cost and registration route. Do not invent missing details.  
> **Format:** Use a short heading, one opening sentence, four bullets and a contact line.  
> **Quality check:** After the announcement, add `Not stated in the source:` followed by any relevant detail the source does not provide.  
> `<source>`  
> [Paste the common source here.]  
> `</source>`

Save the response as **Run B**.

### Step 6.4: Compare Run A and Run B

Compare them using these questions:

- Which response preserved more exact facts?
- Which response followed a more predictable structure?
- Did either response invent information?
- Which prompt component caused each improvement?
- Did the structured prompt guarantee a perfect answer?

### Example improvement conversation

**Student:** Write a notice about a workshop.

**AI:** Join our exciting workshop next week! Certificates and refreshments will be provided.

**Student:** The source did not mention certificates or refreshments. Remove both claims. Use only supplied facts, and add a `Not stated` line for unavailable information.

**AI:** Revised. The notice now uses only the supplied facts and identifies certificates and refreshments as not stated.

**What this demonstrates:** A useful follow-up identifies the exact unsupported claims and the rule that the revision must follow.

---

## Part 7 — Zero-shot and few-shot prompting

### Step 7.1: Zero-shot classification

Open a new chat and enter:

> Classify each message as `ACCESS`, `SCHEDULE`, `TECHNICAL`, or `OTHER`. Return the message ID and one label only.  
> Q1: “Has the workshop room changed?”  
> Q2: “The Events page will not load.”  
> Q3: “Can a second-year student attend?”  
> Q4: “Will lunch be provided?”

This is zero-shot because no completed example is supplied.

### Step 7.2: Few-shot classification

Start another new chat. Use the same task but add these examples before Q1–Q4:

> Example: “My portal says I am not eligible to register.” → `ACCESS`  
> Example: “The registration button gives error 503.” → `TECHNICAL`

This is few-shot because the prompt contains a small number of demonstrations.

### Step 7.3: Compare

Check:

- Did the examples change any label?
- Did they improve format consistency?
- Was every example relevant and consistently formatted?
- Could an incorrect example make the result worse?

### Example chat

**Student:** Label the message: “The page crashes when I select Events.”

**AI:** Website Problem.

**Student:** Use only these labels: `ACCESS`, `SCHEDULE`, `TECHNICAL`, or `OTHER`. Example: “The button returns an error” → `TECHNICAL`. Classify the original message again and return one label only.

**AI:** TECHNICAL

**What this demonstrates:** Constraints prevent a new label, while the example demonstrates the intended mapping and output.

---

## Part 8 — Test grounding and hallucination

Continue from the chat containing the common source.

### Step 8.1: Ask an answerable question

> Is participation free?

Ask the model to quote or point to the exact source fact supporting the answer.

### Step 8.2: Ask an unanswerable question

> Will transport be provided?

If the model says yes or no, ask:

> Point to the exact sentence in the supplied source that supports that claim. If no sentence supports it, correct the answer.

### Step 8.3: Add a grounding rule

Start a new chat and enter:

> Answer using only the supplied source. If the answer is absent, respond exactly: `Not stated in the supplied source.` Question: Will transport be provided? [Paste the source.]

### Expected observation

The grounded prompt makes the acceptable behavior clearer, but you must still inspect the response. A language model generates a plausible continuation; it is not automatically a verified database of facts.

---

## Part 9 — Iterate by naming one defect

Select one imperfect result from the activity. Do not write only `make it better`.

Use this pattern:

> The previous response failed this requirement: **[state the exact requirement]**. Revise only the affected part. Preserve **[state what should not change]**. Check the revision against **[the source, label set, length, or required format]** before answering.

Possible defects:

- one required fact is missing;
- an unsupported fact was added;
- the response is too advanced for the audience;
- the requested table or bullets were not followed;
- the label is outside the allowed set; or
- the answer is too long.

### Checkpoint

A successful revision should fix the named problem without damaging correct parts of the earlier answer.

---

## Part 10 — Compare model outputs carefully

Compare your structured prompt result with another group using either a different application or a new chat in the same application.

Record only these observations:

- application and displayed model;
- whether the same prompt was used;
- important factual differences;
- formatting differences;
- unsupported claims;
- which result better met the stated requirements; and
- one reason why a single test cannot establish that one application is always better.

Possible reasons for variation include different models, model versions, hidden system instructions, chat history and probabilistic token generation.

> Compare responses for the task, not brands in general.

---

## Part 11 — Understand Google's generative AI tools

No Google Cloud access is required. This part uses documentation and a free chat only.

### Step 11.1: Ask for a first explanation

Enter:

> Compare the Gemini chat application, Google AI Studio, Vertex AI and Model Garden for a beginner. For each, explain the main user, purpose and whether it is mainly a chat experience, a prototyping environment, a managed cloud platform, or a model library. Do not provide pricing claims.

### Step 11.2: Verify with current documentation

Check the response against the official links below. Correct any outdated or mixed-up statement.

- **Gemini app:** a conversational application for interacting with Gemini.
- **Google AI Studio:** an environment for trying Gemini models and experimenting with prompts before building with the Gemini API.
- **Vertex AI:** a managed Google Cloud platform for building and operating AI applications and workflows.
- **Model Garden:** a library for discovering and working with Google, open and partner models within Google's AI platform ecosystem.

### Step 11.3: Explain the boundary

Answer this question in your own words:

> Why can this activity teach prompt design in a free Gemini, ChatGPT or Copilot chat, while a real Vertex AI deployment requires a different environment and workflow?

### Important distinction

- **Prompt engineering** changes the text instructions, examples, context and requested output without changing the model's learned parameters.
- **Prompt tuning** is a parameter-efficient training or customization technique that learns task-specific prompt representations. Ordinary free chat interaction is not prompt tuning.

---

## Part 12 — Final challenge: build a verified mini study guide

Create one prompt that asks your chat model to produce a one-page beginner study guide containing all of the following:

1. generative AI compared with traditional ML;
2. GAN, VAE, diffusion and Transformer central ideas;
3. definition of an LLM;
4. tokens and embeddings;
5. Transformer and attention;
6. zero-shot and few-shot prompting;
7. prompt engineering compared with prompt tuning; and
8. four LLM use cases.

Your prompt must include:

- the intended audience;
- a clear output structure;
- a length boundary;
- a request for one relatable example per major section;
- an instruction to mark uncertain or version-sensitive information;
- a final five-question self-check; and
- a requirement that the answer be checked against the official references below.

After receiving the result:

1. inspect every definition;
2. correct at least one unclear sentence through a focused follow-up;
3. check whether the examples actually match the concepts;
4. confirm that prompt engineering was not described as model training; and
5. confirm that the guide does not claim to reveal actual hidden model reasoning.

Do not copy the generated guide without reviewing it. The completed learning outcome is the **design–run–inspect–revise–verify** process.

---

## Troubleshooting guide

### The response is too long

Add a measurable constraint such as a word range, number of bullets, number of table rows or number of sentences.

### The response is too technical

State the audience and assumed knowledge. Ask the model to define unavoidable new terms and use one familiar analogy.

### The model ignores the required format

Place the format on a separate line, supply a short example, and explicitly state which extra content must be omitted.

### The model invents facts

Limit it to the supplied source, ask it to mark missing information, and require a source-fact check after the response.

### A classification label is inconsistent

Define the allowed labels, prohibit new labels and provide one or two consistently formatted examples.

### Different groups obtain different answers

Confirm that the prompt and source are identical, that a new chat was used, and that model/app names were recorded. Some variation can remain even under controlled conditions.

### A free usage limit is reached

Use the standard model offered by the application, continue later when the limit resets, or compare with a teammate's permitted free chat. Do not purchase a plan for this activity.

## Expected outcome

At completion, you should have:

- explored the Unit 1 concept hierarchy and generative-model families;
- connected tokens, embeddings, attention and Transformers to LLM inference;
- performed generation, summarization, extraction, question answering and classification;
- compared vague, structured, zero-shot and few-shot prompts;
- found or tested for an unsupported claim;
- improved a response with a focused follow-up;
- compared two controlled chat results; and
- distinguished consumer chat applications from AI Studio, Vertex AI and Model Garden.

## Completion checklist

- [ ] I used only fictional or non-sensitive information.
- [ ] I recorded the application and displayed model used.
- [ ] I explained the relationship among AI, ML, deep learning and generative AI.
- [ ] I distinguished generation from classification.
- [ ] I compared GANs, VAEs, diffusion models and Transformers.
- [ ] I explored tokens, embeddings, attention and next-token generation.
- [ ] I completed at least four LLM use cases using the common source.
- [ ] I compared a vague prompt with a structured prompt.
- [ ] I performed both zero-shot and few-shot prompting.
- [ ] I tested an answerable and an unanswerable source question.
- [ ] I revised one response by naming a specific defect.
- [ ] I compared outputs under controlled conditions.
- [ ] I distinguished prompt engineering from prompt tuning.
- [ ] I explained Gemini, Google AI Studio, Vertex AI and Model Garden at a beginner level.
- [ ] I completed and verified the final mini study-guide challenge.

---

**Completion standard:** The activity is complete when you can explain the main Unit 1–2 concepts, design a structured prompt, test the resulting response against a source or defined requirements, and improve the prompt using evidence from the result.

## Reference documentation

### Generative AI, LLMs and prompting

- [Google Cloud: What is generative AI?](https://cloud.google.com/discover/what-is-generative-ai)
- [Google Machine Learning Glossary: Generative AI](https://developers.google.com/machine-learning/glossary/generative)
- [Google Machine Learning Crash Course: Large Language Models](https://developers.google.com/machine-learning/crash-course/llm)
- [Google Machine Learning Crash Course: Fine-tuning, distillation and prompt engineering](https://developers.google.com/machine-learning/crash-course/llm/tuning)
- [Google: Prompt design strategies](https://ai.google.dev/gemini-api/docs/prompting-strategies)
- [Google: Using LLMs in technical writing](https://developers.google.com/tech-writing/two/llms)
- [Google Machine Learning: Generative Adversarial Networks](https://developers.google.com/machine-learning/gan)

### Google tools

- [Gemini API documentation](https://ai.google.dev/gemini-api/docs)
- [Google AI Studio quickstart](https://ai.google.dev/gemini-api/docs/ai-studio-quickstart)
- [Generative AI on Vertex AI](https://docs.cloud.google.com/vertex-ai/generative-ai/docs)
- [Vertex AI Model Garden overview](https://cloud.google.com/vertex-ai/generative-ai/docs/model-garden/explore-models)

### Free chat access and limits

- [ChatGPT Learn](https://learn.chatgpt.com/)
- [Microsoft Support: Microsoft Copilot free compared with Microsoft 365 Copilot](https://support.microsoft.com/en-us/microsoft-365-copilot/what-s-the-difference-between-microsoft-copilot-free-and-copilot-in-microsoft-365)
- [Gemini Apps Help: limits and upgrades](https://support.google.com/gemini/answer/16275805)

Documentation and free-access conditions checked on 7 September 2026. Product names, model availability and usage limits can change.
