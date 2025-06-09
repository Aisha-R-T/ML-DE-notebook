## 🧠 Google Prompting Essentials – Reference Notes

*Note that some of this particular set of Notes was rendered by ChatGPT. Much of this material was originally written in PDF or image format.*

## 🔺 Prompting Framework: TCR-EI

Remember it as:

**T**ask  
**C**ontext  
**R**eferences  
**E**valuate  
**I**terate  

---

## 1. 🛠️ Task

Define what you want the model to do.

- Be explicit about **persona** and **format**
- Say what kind of **conversation** or **interaction style** you want (e.g. coaching, 
collaborative)
- Include stop phrases or boundaries if needed (usually only relevant with Gems or custom GPTs)

> ✅ *Example:*  
> You're a science expert designing a college curriculum. Write 2 engaging paragraphs on how 
> DNA was discovered and its impact, in a way that’s clear for beginners. Past students said 
> this topic felt dry; your explanation should be attention-grabbing.

---

## 2. 🧠 Context

Oversharing is good, but you have to be mindful of token limits because that can cause your 
model to ignore parts of your query.

- Provide background, goals, known failures, audience type, and constraints
- Basically, explain the scenario
- If you're looking for an audio/image output (multimodal), make sure to indicate that!

> ✍️ Use delimiters like:
> - Triple quotes: `"""`
> - Tags: `<task>...</task>`
> - Markdown: `**bold**`, `_italic_`
> - Or my favorite signal: `->'
> These guide the model's attention. Useful for separating ideas or requirements

---

## 3. 📚 References

Examples help steer tone, structure, or content—but **only if they’re targeted**.

- Include 2–5 relevant examples, max (more can confuse the model)
- Always explain *why* each reference matters
- Can include text, images, audio, or links (multimodal again)

> 🧠 Multimodal examples can give some unexpected results, in a good way.  
> Combine formats like:
> - 📄 Text + 🎧 Audio  
> - 📷 Image + scenario description  
> Just be clear about **what** you're giving and **why** it matters.

---

## 4. ✅ Evaluate

Don't just glance at the output. Assess:

- Did it follow the task format?
- Did it capture the right tone, voice, and structure?
- Were your references and context actually reflected?
- Does the reasoning hold up?
> This process is pretty easy if you know what your goal is.

If the model fails the evaluation stage, isolate what failed:
- Weak task phrasing?
- Irrelevant reference?
- Not enough context?

> 🔍 You can also ask the model to **evaluate itself**  
> → “What would improve this output?”  
> → “Summarize key takeaways from this conversation.”  
> → “Explain how you reached this result.” *(Chain-of-thought prompting)*

---

## 5. 🔁 Iterate (ABI: Always Be Iterating)

Make changes based on what didn’t work.

Ways to iterate:
- Revisit your **persona + format** definition
- Adjust context: clarify goals, reword constraints
- Break your prompt into **smaller, sequential parts**
- Switch to an **analogous version** of the task to reframe

> 🪵 Tree-of-thought prompting: Ask the model to show alternate paths it considered.

> 🔁 Prompt chaining: Use the output of one prompt as **input context** for the next.

---

## 🧾 Extra Reminders

- **Get approval** from your team before using AI in company/client work  
- **Disclose AI use** if needed—transparency matters!
- **Consider privacy and security** before sharing sensitive info!!! VERY important!
- AI is a collaborator, not an oracle. Prompting is a process, not a shortcut.

---

## 🧩 Short Summary of Techniques

- **Design an AI agent** for specific use (e.g., editor, critic, coach)  (Gems)
- **Compare outputs** by asking the tool to generate multiple variations  
- **Ask for reasoning** to improve clarity or debug bad output  
- **Use stop phrases** to exit or end conversations cleanly (mostly relevant for Gems)

---

## 🔐 Responsible Use Checklist (because, again, very important!)

- [ ] Got permission to use AI on this task?
- [ ] Thought about privacy/security?
- [ ] Did I disclose AI use if this output goes public?
- [ ] Is the result usable, accurate, and not misleading?


---


### 🧩 Prompt Refinement Strategies

**Leveling up**  
Ask the gen AI tool directly how to improve your prompt.  
From: *I'm working on an ad campaign for a local auto body shop’s sale on tires and windshields. Generate an announcement for the sale.*  
To: *How can I change my initial prompt to produce an ad campaign that uses more engaging language and creates a more memorable impression?*

**Remixing**  
If you have multiple prompts missing different details, ask the model to synthesize them into a single "super prompt."

**Style swap**  
Adjust mood/tone. If your prompt is returning technically correct but dull answers, tell the model to rewrite with a more emotional or vivid delivery.

---

**Direct generation**  
You can literally ask the model to generate a prompt for you.  
Example: *Generate a prompt that could help write a job offer letter to our top candidates.*

**Template request**  
Ask the model to return a prompt **outline** instead of a finished prompt.  
Example: *Create a template specifying the most important elements of a gen AI prompt meant to plan travel for a baseball team.*

**Image-based prompting**  
Paste an image and write: *Generate a prompt I can use to create a logo for my dog food company that evokes the style of the attached image.*

**Text-based prompting**  
Upload or paste text (e.g., from a manual), then say:  
*Using the text, generate a prompt to begin an explanation of the most important concepts.*

**Meta-prompt chaining**  
Break big prompt construction into steps.  
Example:  
*Generate a prompt that identifies the most important qualities of an intelligent and accessible intro paragraph for a grant proposal.*  
Then use that output to write your next prompt.

---

### 🤖 Design AI Agents (Gems especially)

To create a persistent AI agent, layer in:
- **Persona**: e.g., "Act like a personal fitness trainer and nutritionist"
- **Context**: "I'm looking to adopt a healthier lifestyle"
- **Conversation type**: "Ask about routines, give feedback"
- **Stop phrase**: "When I write ‘no pain, no gain,’ end the session"
- **Takeaway prompt**: "At the end, summarize the advice you gave"

Visuals like color-coded block layouts can help you remember what each part does in your agent instructions.

---

### 🎛️ Top-k Sampling

Top-k controls **how many tokens the model chooses from**, affecting randomness and creativity.

- **Top-k = 1** → Greedy decoding: Most deterministic result, always the same
- **Lower top-k** → Narrower range = fewer hallucinations
- **Higher top-k** → Broader range = more creative or unexpected outputs

Use lower top-k for reliability (e.g., summarizing docs), higher top-k for creativity (e.g., product names, campaign slogans).

---


### Things I have found helpful:

1. Depending on prompt complexity, sometimes nesting roles can help. 

- **Example:** telling the model that it is an expert communicator and it needs to determine 
the ideal response to a client's question will allow the model freedom to be creative. If you 
need the model to follow a strict set of instructions instead, you can start off with 
something like: 
> "You are being evaluated on your ability to follow strict formatting and style rules.
> This is not a creative task. The output must match the rule set exactly.
> Any deviation from the format or rule set is considered a task failure."